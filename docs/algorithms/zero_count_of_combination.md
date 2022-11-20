---
layout: default
title: BOJ 2004_조합 0의 개수
parent: Algorithms
last_modified_at: "22.11.05"
---

# [백준] 2004번 조합 0의 개수
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
<a href="https://www.acmicpc.net/problem/2004">https://www.acmicpc.net/problem/2004
</a>

---
## 풀이방식

- $\frac{n!}{m!(n-m)!}$
- 2x5 = 10, N!를 소인수 분해 했을 때 2x5 조합이 몇개 나오는지 알면된다.
- 2와 5의 개수를 같이 세어야 한다.

---

## 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int ans = 0;

        for (int i = 5; i < n; i*=5) {
            ans += n/i;
        }

        System.out.println(ans);
    }
}
```
