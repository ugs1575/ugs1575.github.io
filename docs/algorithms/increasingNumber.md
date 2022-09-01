---
layout: default
title: BOJ 11057_오르막 수
parent: Algorithms
last_modified_at: "22.09.01"
---

# [백준] 11057번 오르막 수
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
<br>
오르막 수는 수의 자리가 오름차순을 이루는 수를 말한다. 이때, 인접한 수가 같아도 오름차순으로 친다.

예를 들어, 2234와 3678, 11119는 오르막 수이지만, 2232, 3676, 91111은 오르막 수가 아니다.

수의 길이 N이 주어졌을 때, 오르막 수의 개수를 구하는 프로그램을 작성하시오. 수는 0으로 시작할 수 있다.
- 문제링크 :
<a href="https://www.acmicpc.net/problem/11057">https://www.acmicpc.net/problem/11057
</a>

---
## 입력
<br>
첫째 줄에 N (1 ≤ N ≤ 1,000)이 주어진다.

---
## 출력
<br>
첫째 줄에 길이가 N인 오르막 수의 개수를 10,007로 나눈 나머지를 출력한다.

---
## 예제 입력 1

```
입력
1

출력
10
```
## 예제 입력 2
```
입력
2

출력
55
```

## 예제 입력 3
```
입력
3

출력
220
```

---
## 접근 방식
<br>
2차원 배열을 사용할 생각을 못 했던 것 같다.<br>
-1, +1 차이가 나는 숫자가 온다까지 접근은 했는데 이걸 어떻게 코드로 풀어낼까 답이 안 나왔다.

---

## 풀이 방식
- d[n][l] = n 자리 계단이면서 마지막 수가 l인 경우의 수
- d[n][l] = d[n-1][l-1] + d[n-1][l+1]
- n 자리 계단이면서 마지막 수가 l인 경우는 아래 두 가지 경우의 수를 더해주면 된다.
- n-1 자리면서 l보다 1 작은 수가 오는 경우의 수와
- n-1 자리면서 l보다 1 큰 수가 오는 경우의 수
- 주의할 점은 l이 0이거나 9일 때인데 이 부분은 예외 처리를 해주면 된다.

---

## Bottom-up 방식
```java
package dynamic;

import java.util.Scanner;

public class Main {
    public static final long MOD = 10007L;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long[][] d = new long[n+1][10];

        for (int i = 0; i <= 9; i++) {
            d[1][i] = 1L;
        }

        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {
                for (int k = 0; k <= 9; k++) {
                    if (j-k >= 0) {
                        d[i][j] += d[i-1][j-k];
                    }
                }
                d[i][j] %= MOD;
            }
        }

        int ans = 0;
        for (int j = 0; j <= 9; j++) {
            ans += d[n][j];
        }

        System.out.println(ans);
    }
}


```