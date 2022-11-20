---
layout: default
title: BOJ 1463_1로 만들기
parent: Algorithms
last_modified_at: "22.08.27"
---

# [백준] 1463번 1로 만들기
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
<a href="https://www.acmicpc.net/problem/1463">https://www.acmicpc.net/problem/1463
</a>

---
## 풀이방식
한번에 풀었지만 풀이 방식을 다르게 해서 Top-Down 방식으로 다시 풀어보았다.<br>
세가지 연산을 모두 하면서 값을 memoization 해놓았다가 해당값이 있으면 바로 리턴한다.<br>
- d[x] = x가 1이 되는 최소 연산 횟수


---

## Top-Down 방식
```java
import java.util.Scanner;

public class Main {
    public static int[] d;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        d = new int[n+1];
        System.out.println(makeOne(n));
    }

    private static int makeOne(int n) {
        System.out.println(n);
        if (n == 1)
            return 0;

        if (d[n] > 0) {
            return d[n];
        }

        d[n] = makeOne(n-1) + 1;

        if (n%3 == 0) {
            int temp = makeOne(n/3) + 1;
            if (d[n] > temp) {
                d[n] = temp;
            }
        }

        if (n%2 == 0) {
            int temp = makeOne(n/2) + 1;
            if (d[n] > temp) {
                d[n] = temp;
            }
        }

        return d[n];
    }
}
```
## 내가 푼 코드
```java
import java.util.Scanner;

public class Main {
    static int ans = Integer.MAX_VALUE;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();
        makeOne(x, 0);
        System.out.println(ans);
    }

    private static void makeOne(int x, int count) {
        if (x <= 0 || count > ans) {
            return;
        }

        if (x == 1) {
            ans = Math.min(count, ans);
            return;
        }

        if (x % 3 == 0) {
            makeOne(x/3, count+1);
        }

        if (x % 2 == 0) {
            makeOne(x/2, count+1);
        }

        makeOne(x-1, count+1);
    }
}
```