---
layout: default
title: BOJ 10844_쉬운 계단 수
parent: Algorithms
last_modified_at: "22.08.31"
---

# [백준] 10844번 쉬운 계단 수
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
45656이란 수를 보자.

이 수는 인접한 모든 자리의 차이가 1이다. 이런 수를 계단 수라고 한다.

N이 주어질 때, 길이가 N인 계단 수가 총 몇 개 있는지 구해보자. 0으로 시작하는 수는 계단수가 아니다.
- 문제링크 :
<a href="https://www.acmicpc.net/problem/10844">https://www.acmicpc.net/problem/10844
</a>

---
## 입력
<br>
첫째 줄에 N이 주어진다. N은 1보다 크거나 같고, 100보다 작거나 같은 자연수이다.

---
## 출력
<br>
첫째 줄에 정답을 1,000,000,000으로 나눈 나머지를 출력한다.

---
## 예제 입력 1

```
입력
1

출력
9
```
## 예제 입력 2
```
입력
2

출력
17
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
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        public static long mod = 1000000000L;

        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            int n = sc.nextInt();
            int[][] d = new int[n+1][10];

            for (int i = 1; i <= 9; i++) {
                d[1][i] = 1;
            }

            for (int i = 2; i <= n; i++) {
                for (int j = 0; j <= 9; j++) {
                    if (j-1 >= 0) {
                        d[i][j] += d[i-1][j-1];
                    }

                    if (j+1 <= 9) {
                        d[i][j] += d[i-1][j+1];
                    }

                    d[i][j] %= mod;
                }
            }

            long ans = 0L;
            for (int i = 0; i <= 9; i++) {
                ans += d[n][i];
            }

            ans %= mod;
            System.out.println(ans);
        }

    }
}

```