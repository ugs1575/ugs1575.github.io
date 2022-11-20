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
## 문제링크
<a href="https://www.acmicpc.net/problem/9465">https://www.acmicpc.net/problem/9465
</a>

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