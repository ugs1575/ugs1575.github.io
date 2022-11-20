---
layout: default
title: BOJ 11053_증가하는 부분 수열
parent: Algorithms
last_modified_at: "22.09.17"
---

# [백준] 11053번 증가하는 부분 수열
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
<a href="https://www.acmicpc.net/problem/11053">https://www.acmicpc.net/problem/11053
</a>

---
## 풀이 방식
- d[i] = 1~i까지 있을 때, i번째 수를 마지막으로 하는 가장 긴 증가하는 부분 수열 길이
- 위 처럼 정의 했을 때, 1 <= j, i-1 <= j라고 하면 j의 범위를 for문을 돌면서 i번째 수보다 j번째 수가 작으면 d[j] + 1을 해서 가장 최대값을 d[i]에 넣어주면 된다. 

---

## 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] numbers = new int[n];
        int[] d = new int[n];

        for (int i = 0; i < n; i++) {
            numbers[i] = sc.nextInt();
        }

        for (int i = 0; i < n ; i++) {
                d[i] = 1;
            for (int j = 0; j < i; j++) {
                if (numbers[j] < numbers[i] && d[i] < d[j] + 1) {
                    d[i] = d[j] + 1;
                }
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans = Math.max(ans, d[i]);
        }


        System.out.println(ans);
    }
}
```


