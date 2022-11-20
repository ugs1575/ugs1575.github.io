---
layout: default
title: BOJ 2193_이친수
parent: Algorithms
last_modified_at: "22.09.08"
---

# [백준] 2193번 이친수
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
<a href="https://www.acmicpc.net/problem/2193">https://www.acmicpc.net/problem/2193
</a>

---
## 풀이 방식 1 (이차원 배열 사용)
- d[n][l] = n 자리이면서 마지막 자리가 l인 경우의 수로 정의했다.
- l은 0 또는 1이 올 수 있다.
- n자리이면서 끝자리가 0이면, n-1자리 이면서 끝자리가 0 또는 1이 되어야 한다.
- n자리이면서 끝자리가 1이면, n-1자리 이면서 끝자리가 0이되어야 한다.

다음을 식으로 표현하면
- d[n][0] = d[n-1][1] + d[n-1][0]
- d[n][1] = d[n-1][0]
정답은 n자리이면서 끝자리가 0인 경우의 수와 n자리면서 끝자리가 1인 경우의 수를 더해주면 된다.
- answer = d[n][0] + d[n][1]

## 풀이 방식1 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long[][] d = new long[n+1][2];
        d[1][1] = 1L;

        for (int i = 2; i <= n; i++) {
            d[i][0] = d[i-1][1] + d[i-1][0];
            d[i][1] = d[i-1][0];
        }

        long ans = d[n][0] + d[n][1];
        System.out.println(ans);
    }
}
```

---

## 풀이 방식 2 (일차원 배열 사용)
- d[n] = n자리 이친수의 갯수
  - d[n]을 구하기 위해서 2가지 방법을 생각해 볼 수 있는데
  1. n자리 이친수 인데 끝에 0이 오는 경우의 수 
  2. 끝에 1이 오는 경우의 수
  - 결국 d[n]을 구하기 위해서는 두가지 경우의 수를 더해주면 된다.

- n자리 이친수 끝에 0이 온다고 한다면 n-1자리에는 0과 1둘다 올 수 있다. 
- 결국 d[n-1]에 0을 붙이는 것과 같다고 볼 수 있다.
- n자리 이친수 끝에 1이 온다고 한다면 n-2자리에 01을 붙이는 것과 같다.
- 결국 d[n-1]에 01을 붙인다고 생각볼 수 있다.

결론적으로 다음과 같이 정의 할 수 있다.
- d[n] = d[n-1] + d[n-2]


## 풀이 방식2 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long[] d = new long[n+1];

        d[1] = 1L;
        if (n >= 2) {
            d[2] = 1L;
        }
        for (int i = 3; i <= n; i++) {
            d[i] = d[i-1] + d[i-2];
        }

        System.out.println(d[n]);
    }
}


```