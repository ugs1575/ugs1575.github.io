---
layout: default
title: BOJ 11052_카드 구매하기
parent: Algorithms
last_modified_at: "22.08.30"
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
## 문제링크
<a href="https://www.acmicpc.net/problem/11052">https://www.acmicpc.net/problem/11052
</a>

---
## 풀이 방식
- d[i] = i개의 카드를 구매할 수 있는 최댓값
- 겹치는 부분을 찾는 것이 중요한 것 같다.
- 1개를 살 때 최댓값은 1개 카드팩의 가격이다.
- 2개를 가능한 최댓값을 구해보자!
    1. 1개를 살때 최댓값 + 남은 개수를 살때 최댓값 즉 2-1 = 1개를 살때 최댓값을 더해준다.
    2. 2개 카드팩을 산다
    - 1번 2번 중 최댓값을 선택한다.
- 3개를 가능한 경우의 수를 생각해보자!
    1. 1개를 살 때 최댓값 + (3-1) 개를 살때 최댓값
    2. 2개를 살 때 최댓값 + (3-2) 개를 살때 최댓값
    3. 3개 팩을 산다.

이런식으로 생각해보면 될 것 같다.

---

## Bottom-up 방식
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] p = new int[n+1];
        int[] d = new int[n+1];

        for (int i = 1; i <= n; i++) {
            p[i] = sc.nextInt();
            d[i] = p[i];
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                d[i] = Math.max(d[j] + d[i-j], d[i]);
            }
        }

        System.out.println(d[n]);

    }
}

```