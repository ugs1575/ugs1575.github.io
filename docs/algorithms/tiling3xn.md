---
layout: default
title: BOJ 2133_타일채우기
parent: Algorithms
last_modified_at: "22.09.22"
---

# [백준] 2133번 타일채우기
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
<a href="https://www.acmicpc.net/problem/2133">https://www.acmicpc.net/problem/2133
</a>

---

## 접근 방식
- 3x2를 채우는 경우의 수를 생각해보면 3가지가 나오고
- 3x4를 생각해봤을 때 3x2를 채우는 경우의 수를 일단 먼저 채우고 나머지 3x2의 면적을 똑같은 경우의 수로 채우면 되지 않을까 생각했는데 예외가 있었다.
- 예외를 어떻게 처리할까 하다가.. 결국 풀지 못 했다.

---

## 풀이 방식
- d[n] = 3xn 크기의 벽을 2x1, 1x2 크기의 타일로 채우는 경우의 수
- d[n] = 3*d[n-2] + 2*d[n-4] + 2*d[n-6] ... + 2*d[0] (항상 2개씩 예외가 있다.)

---

## 풀이 방식
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] d = new int[n+1];

        d[0] = 1;
        if (n > 1) {
            d[2] = 3;
        }
        for (int i = 3; i <= n ; i++) {
            d[i] = 3*d[i-2];
            for (int j = 4; j <= i; j+=2) {
                d[i] += 2*d[i-j];
            }
        }

        System.out.println(d[n]);
    }
}

```