---
layout: default
title: BOJ 2579_계단오르기
parent: Algorithms
last_modified_at: "22.09.19"
---

# [백준] 2579번 계단오르기
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
계단 오르기 게임은 계단 아래 시작점부터 계단 꼭대기에 위치한 도착점까지 가는 게임이다. <그림 1>과 같이 각각의 계단에는 일정한 점수가 쓰여 있는데 계단을 밟으면 그 계단에 쓰여 있는 점수를 얻게 된다.


<p align="center"><img src="https://upload.acmicpc.net/7177ea45-aa8d-4724-b256-7b84832c9b97/-/preview/"></p>
<그림 1>
<br><br>
예를 들어 <그림 2>와 같이 시작점에서부터 첫 번째, 두 번째, 네 번째, 여섯 번째 계단을 밟아 도착점에 도달하면 총 점수는 10 + 20 + 25 + 20 = 75점이 된다.


<p align="center"><img src="https://upload.acmicpc.net/f00b6121-1c25-492e-9bc0-d96377c586b0/-/preview/"></p>
<그림 2>

계단 오르는 데는 다음과 같은 규칙이 있다.

1. 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면서 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.
2. 연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.
3. 마지막 도착 계단은 반드시 밟아야 한다.
따라서 첫 번째 계단을 밟고 이어 두 번째 계단이나, 세 번째 계단으로 오를 수 있다. 하지만, 첫 번째 계단을 밟고 이어 네 번째 계단으로 올라가거나, 첫 번째, 두 번째, 세 번째 계단을 연속해서 모두 밟을 수는 없다.

각 계단에 쓰여 있는 점수가 주어질 때 이 게임에서 얻을 수 있는 총 점수의 최댓값을 구하는 프로그램을 작성하시오.


- 문제링크 :
<a href="https://www.acmicpc.net/problem/2579">https://www.acmicpc.net/problem/2579
</a>

---
## 입력
입력의 첫째 줄에 계단의 개수가 주어진다.

둘째 줄부터 한 줄에 하나씩 제일 아래에 놓인 계단부터 순서대로 각 계단에 쓰여 있는 점수가 주어진다. 계단의 개수는 300이하의 자연수이고, 계단에 쓰여 있는 점수는 10,000이하의 자연수이다.

---
## 출력
첫째 줄에 계단 오르기 게임에서 얻을 수 있는 총 점수의 최댓값을 출력한다.

---
## 예제 입력 1

```
입력
6
10
20
15
25
10
20

출력
75
```

---
## 접근 방식
i 번째 계단을 밟았을 때, 밟지 않았을 때로 나누어 생각하니까 잘 안 풀렸다. <br>
연속 조건이 붙을 때는 몇 번째 연속으로 접근해서 생각해야 할 거 같다.

---
## 풀이 방식
- d[i][j] = i 번째 계단을 j 번 연속해서 올라갔을 때 최댓값
- d[i][0] = i 번째 계단을 0번째 연속해서 올라갔을 때 => 불가능
- d[i][1] = i 번째 계단을 1번째 연속해서 올라갔을 때
- i-1 번째를 올라가지 않아야 함, i-2 번째는 몇 번째든 상관없다.
- MAX(d[i-2][1] + stair[i], d[i-2][2] + stair[i])
- d[i][2] = i 번째 계단을 2번째 연속해서 올라갔을 때
- i-1 번째를 올라갔어야 함, i-2 번째는 올라가지 않았어야 함.
- d[i-1][1] + stair[i]

---

## 풀이 방식1 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] d = new int[n+1][3];
        int[] stairs = new int[n+1];

        for (int i = 1; i <= n; i++) {
            stairs[i] = sc.nextInt();
        }

        d[1][1] = stairs[1];
        d[1][2] = stairs[1];
        for (int i = 2; i <= n; i++) {
            d[i][1] = Math.max(d[i-2][1] + stairs[i], d[i-2][2] + stairs[i]);
            d[i][2] = d[i-1][1] + stairs[i];
        }

        System.out.println(Math.max(d[n][1], d[n][2]));
    }
}
```
