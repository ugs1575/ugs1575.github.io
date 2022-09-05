---
layout: default
title: BOJ 11057_오르막 수
parent: Algorithms
last_modified_at: "22.09.05"
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
- d[n][l] = n 자리이면서 마지막 자리가 l인 경우의 수로 정의했다.
- 오르막 수는 현재 자리보다 이전 자리에 같은 숫자 또는 작은 숫자가 오면 된다.

나는 이걸 아래와 차이로 접근해서 틀려버렸다
d[n][l] = d[n-1][l-0] + d[n-1][l-9] ..

또 마지막에 전체 합을 구하는 부분에서 integer 타입으로 정의하고 10007로 나눈 나머지 값을 구하지 않았다.

어차피 n-1 자리의 마지막 수는 0부터 l까지의 값이 되기 때문에 굳이 차이로 접근하지 않아도 됐었다.

---

## Bottom-up 방식
```java
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
                for (int k = 0; k <= j; k++) {
                    d[i][j] += d[i-1][k];
                }
                d[i][j] %= MOD;
            }
        }

        long ans = 0L;
        for (int j = 0; j <= 9; j++) {
            ans += d[n][j];
        }
        ans %= MOD;
        System.out.println(ans);
    }
}


```