---
layout: default
title: BOJ 9561_파도반수열
parent: Algorithms
last_modified_at: "22.09.23"
---

# [백준] 9561번 파도반수열
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
<a href="https://www.acmicpc.net/problem/9561">https://www.acmicpc.net/problem/9561
</a>

---
## 풀이 방식
- 그림을 보면 규칙을 찾을 수 있다.
- d[i] = i번째 변의 길이 
- d[i] = d[i-1] + d[i-5]

---

## 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int tc = sc.nextInt();
        long[] d = new long[101];

        d[1] = 1L;
        d[2] = 1L;
        d[3] = 1L;
        d[4] = 2L;

        for (int i = 0; i < tc; i++) {
            int n = sc.nextInt();

            for (int j = 5; j <= n; j++) {
                d[j] = d[j-1] + d[j-5];
            }

            System.out.println(d[n]);
        }

    }
}
```