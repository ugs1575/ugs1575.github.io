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
## 문제
<br>
0과 1로만 이루어진 수를 이진수라 한다. 이러한 이진수 중 특별한 성질을 갖는 것들이 있는데, 이들을 이친수(pinary number)라 한다. 이친수는 다음의 성질을 만족한다.

이친수는 0으로 시작하지 않는다.
이친수에서는 1이 두 번 연속으로 나타나지 않는다. 즉, 11을 부분 문자열로 갖지 않는다.
예를 들면 1, 10, 100, 101, 1000, 1001 등이 이친수가 된다. 하지만 0010101이나 101101은 각각 1, 2번 규칙에 위배되므로 이친수가 아니다.

N(1 ≤ N ≤ 90)이 주어졌을 때, N자리 이친수의 개수를 구하는 프로그램을 작성하시오.


- 문제링크 :
<a href="https://www.acmicpc.net/problem/2193">https://www.acmicpc.net/problem/2193
</a>

---
## 입력
<br>
첫째 줄에 N이 주어진다.

---
## 출력
<br>
첫째 줄에 N자리 이친수의 개수를 출력한다.

---
## 예제 입력 1

```
입력
3

출력
2
```

---
## 풀이 방식 1
<br>
- d[n][l] = n 자리이면서 마지막 자리가 l인 경우의 수로 정의했다.
- l은 0 또는 1이 올 수 있다.
- n자리이면서 끝자리가 0이면, n-1자리 이면서 끝자리가 0 또는 1이 되어야 한다.
- n자리이면서 끝자리가 1이면, n-1자리 이면서 끝자리가 0이되어야 한다.

다음을 식으로 표현하면
- d[n][0] = d[n-1][1] + d[n-1][0]
- d[n][1] = d[n-1][0]
정답은 n자리이면서 끝자리가 0인 경우의 수와 n자리면서 끝자리가 1인 경우의 수를 더해주면 된다.
- answer = d[n][0] + d[n][1]

---

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

## 풀이 방식 2
<br>

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
---

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