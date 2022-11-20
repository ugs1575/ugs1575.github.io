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
## 문제링크
<a href="https://www.acmicpc.net/problem/2579">https://www.acmicpc.net/problem/2579
</a>

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
