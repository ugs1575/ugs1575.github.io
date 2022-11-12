---
layout: default
title: BOJ 9465_스티커
parent: Algorithms
last_modified_at: "22.09.07"
---

# [백준] 9465번 스티커
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---
## 문제
상근이의 여동생 상냥이는 문방구에서 스티커 2n개를 구매했다. 스티커는 그림 (a)와 같이 2행 n열로 배치되어 있다. 상냥이는 스티커를 이용해 책상을 꾸미려고 한다.

상냥이가 구매한 스티커의 품질은 매우 좋지 않다. 스티커 한 장을 떼면, 그 스티커와 변을 공유하는 스티커는 모두 찢어져서 사용할 수 없게 된다. 즉, 뗀 스티커의 왼쪽, 오른쪽, 위, 아래에 있는 스티커는 사용할 수 없게 된다.

<p align="center"><img src="https://www.acmicpc.net/upload/images/sticker.png"></p>

모든 스티커를 붙일 수 없게된 상냥이는 각 스티커에 점수를 매기고, 점수의 합이 최대가 되게 스티커를 떼어내려고 한다. 먼저, 그림 (b)와 같이 각 스티커에 점수를 매겼다. 상냥이가 뗄 수 있는 스티커의 점수의 최댓값을 구하는 프로그램을 작성하시오. 즉, 2n개의 스티커 중에서 점수의 합이 최대가 되면서 서로 변을 공유 하지 않는 스티커 집합을 구해야 한다.

위의 그림의 경우에 점수가 50, 50, 100, 60인 스티커를 고르면, 점수는 260이 되고 이 것이 최대 점수이다. 가장 높은 점수를 가지는 두 스티커 (100과 70)은 변을 공유하기 때문에, 동시에 뗄 수 없다.
- 문제링크 :
<a href="https://www.acmicpc.net/problem/9465">https://www.acmicpc.net/problem/9465
</a>

---
## 입력
첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스의 첫째 줄에는 n (1 ≤ n ≤ 100,000)이 주어진다. 다음 두 줄에는 n개의 정수가 주어지며, 각 정수는 그 위치에 해당하는 스티커의 점수이다. 연속하는 두 정수 사이에는 빈 칸이 하나 있다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다. 

---
## 출력
각 테스트 케이스 마다, 2n개의 스티커 중에서 두 변을 공유하지 않는 스티커 점수의 최댓값을 출력한다.

---
## 예제 입력 1

```
입력
2
5
50 10 100 20 40
30 50 70 10 60
7
10 30 10 50 100 20 40
20 40 30 50 60 20 80

출력
260
290
```
---
## 풀이 방식
- d[n][i] = 2xn개의 스티커 중에 n번째 열을 전부떼어내거나, 위 또는 아래만 떼어낸 경우 최댓값
    1. i = 0, n번째 열을 전부 떼어낸다.
    2. i = 1, n번째 열에서 위 스티커만 떼어낸다.
    3. i = 2, n번째 열에서 아래 스티커만 떼어낸다.
- d[n][0] = max(d[n-1][0], d[n-1][1], d[n-1][2])
    - n번째 열을 전부 떼어낸다면 n-1번째 열은 1,2,3 번 행위가 전부 가능하다.
- d[n][1] = max(d[n-1][0], d[n-1][2]) + sticker[0][n-1];
    - n번째 열의 위만 떼어낸다면 n-1번째 열은 1,3 번 행위만 가능하다.
    - n번째 열의 위 스티커 점수만 더해주면 된다.
- d[n][2] = max(d[n-1][0], d[n-1][1]) + sticker[0][n-1];
    - n번째 열의 아래만 떼어낸다면 n-1번째 열은 1,2 번 행위만 가능하다.
    - n번째 열의 아래 스티커 점수만 더해주면 된다.

---

## Bottom-up 방식
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();

        for (int i = 0; i < t; i++) {
            int n = sc.nextInt();
            int[][] stickers = new int[3][n+1];

            for (int j = 1; j <= 2; j++) {
                for (int k = 1; k <= n; k++) {
                    stickers[j][k] = sc.nextInt();
                }
            }

            int[][] d = new int[n+1][3];

            for (int j = 1; j <= n; j++) {
                d[j][0] = Math.max(Math.max(d[j-1][0], d[j-1][1]), d[j-1][2]);
                d[j][1] = Math.max(d[j-1][0], d[j-1][2]) + stickers[1][j];
                d[j][2] = Math.max(d[j-1][0], d[j-1][1]) + stickers[2][j];
            }

            int ans = Math.max(Math.max(d[n][0], d[n][1]), d[n][2]);
            System.out.println(ans);
        }
    }
}


```