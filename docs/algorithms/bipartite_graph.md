---
layout: default
title: BOJ 1707_이분 그래프
parent: Algorithms
last_modified_at: "22.11.20"
---

# [백준] 1707번 이분 그래프
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
<a href="https://www.acmicpc.net/problem/1707">https://www.acmicpc.net/problem/1707
</a>

---
## 풀이방식
- 이분 그래프는 같은 집합에 속한 정점끼리는 서로 연결된 간선이 없다는 특징이 있다.
- 색깔로 구분하여 빨간색이 방문한 정점은 파란색으로 체크, 파란색으로 방문한 정점은 반대로 빨간색으로 체크하여 마지막에 같은색끼리 이어진 간선이 있는지 체크하면 이분 그래프인지 아닌지 판단할 수 있다.
- 0 : 방문 안함
- 1 : 방문함, 빨간색
- 2 : 방문함, 파란색

---

## 코드
```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class Main {
    static final int NOT_VISIT = 0;
    static final int BLUE = 1;
    static final int RED = 2;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int k = sc.nextInt();

        for (int i = 0; i < k; i++) {
            int v = sc.nextInt();
            int e = sc.nextInt();

            ArrayList<Integer>[] graph = new ArrayList[v+1];
            for (int j = 1; j <= v; j++) {
                graph[j] = new ArrayList<>();
            }

            for (int j = 0; j < e; j++) {
                int start = sc.nextInt();
                int end = sc.nextInt();
                graph[start].add(end);
                graph[end].add(start);
            }

            int[] visit = new int[v+1];
            for (int j = 1; j <= v; j++) {
                if (visit[j] == NOT_VISIT) {
                    bfs(graph, visit, j);
                }
            }

            boolean bipartiteGraph = isBipartiteGraph(graph, visit, v);

            if (bipartiteGraph) {
                System.out.println("YES");
            } else {
                System.out.println("NO");
            }
        }
    }

    private static boolean isBipartiteGraph(ArrayList<Integer>[] graph, int[] visit, int v) {
        for (int i = 1; i <= v; i++) {
            for (int j = 0; j < graph[i].size(); j++) {
                if (visit[i] == visit[graph[i].get(j)]) {
                    return false;
                }
            }
        }

        return true;
    }

    private static void bfs(ArrayList<Integer>[] graph, int[] visit, int j) {
        Queue<Integer> q = new LinkedList<>();
        visit[j] = BLUE;
        q.add(j);

        while (!q.isEmpty()) {
            int start = q.remove();
            for (int i = 0; i < graph[start].size(); i++) {
                int end = graph[start].get(i);
                if (visit[end] == NOT_VISIT) {
                    visit[end] = 3-visit[start];
                    q.add(visit[end]);
                }
            }
        }

    }
}
```
