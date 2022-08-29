---
layout: default
title: BOJ 11727_2xn 타일링 2
parent: Algorithms
last_modified_at: "22.08.29"
---

# [백준] 11727번 2xn 타일링 2
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
2×n 직사각형을 1×2, 2×1과 2×2 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.

아래 그림은 2×17 직사각형을 채운 한가지 예이다.

<p align="center"><img src="https://www.acmicpc.net/upload/images/t2n2122.gif"></p>

- 문제링크 :
<a href="https://www.acmicpc.net/problem/11727">https://www.acmicpc.net/problem/11727
</a>

---
## 입력
<br>
첫째 줄에 n이 주어진다. (1 ≤ n ≤ 1,000)

---
## 출력
<br>
첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

---
## 예제 입력 1

```
입력
2

출력
3
```
## 예제 입력 2
```
입력
8

출력
171
```
## 예제 입력 3
```
입력
12

출력
2731
```
---
## 풀이 방식

이 문제는 11726번 2xn 타일링 문제와 풀이 방식이 유사하기에 <a href="/docs/algorithms/tiling" style="color: #2c84fa">여기</a>를 참고하면 될 것 같다.<br>

- d[n] = 2xn 면적에 타일을 채우는 방법의 수
1. 마지막에 2x1 타일 한 개 붙이기
2. 1x2타일 2개를 위 아래로 겹쳐서 붙이기
3. 2x2타일 한 개 붙이기 

3가지 방법을 생각하면 된다.<br>
경우의 수를 구하는 것이기 때문에 세가지 방법을 더해주면 된다.

---

## Top-down 방식
```java
import java.util.Scanner;

public class Main {
    public static int[] d;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        d = new int[n+1];
        d[0] = 1;
        d[1] = 1;
        System.out.println(tiling(n));
    }

    private static int tiling(int n) {
        if (d[n] > 0) return d[n];

        d[n] = tiling(n-1) + tiling(n-2) + tiling(n-2);
        d[n] = d[n]%10007;

        return d[n];
    }
}
```
## Bottom-up 방식
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] d = new int[n+1];
        d[0] = 1;
        d[1] = 1;

        for (int i = 2; i <= n; i++) {
            d[i] = d[i-1] + d[i-2];
            d[i] = d[i]%10007;
        }
        System.out.println(d[n]);
    }
}
```