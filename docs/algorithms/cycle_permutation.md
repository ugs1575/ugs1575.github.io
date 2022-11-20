---
layout: default
title: BOJ 10451_순열 사이클
parent: Algorithms
last_modified_at: "22.11.20"
---

# [백준] 10451번 순열 사이클
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
<a href="https://www.acmicpc.net/problem/10451">https://www.acmicpc.net/problem/10451
</a>

---
## 풀이 방식
- 순열이어서 무조건 싸이클이 있을 수 밖에 없다.
- 그래서 방문했던 점을 방문했는지 검사할 필요가 없고 그냥 탐색이 끊어지면 +1 해주면 된다.

---

## 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while (t-- > 0) {
            int v = sc.nextInt();
            int[] graph = new int[v+1];

            for (int j = 1; j <= v; j++) {
                graph[j] = sc.nextInt();
            }

            boolean[] visit = new boolean[v+1];
            int cycle = 0;
            for (int j = 1; j <= v; j++) {
                if (visit[j]) continue;
                dfs(graph, visit, j);
                cycle ++;
            }

            System.out.println(cycle);
        }
    }

    private static void dfs(int[] graph, boolean[] visit, int j) {
        if (visit[j]) return;
        visit[j] = true;
        dfs(graph, visit, graph[j]);
    }
}
```
