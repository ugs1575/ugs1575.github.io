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
## 문제
그래프의 정점의 집합을 둘로 분할하여, 각 집합에 속한 정점끼리는 서로 인접하지 않도록 분할할 수 있을 때, 그러한 그래프를 특별히 이분 그래프 (Bipartite Graph) 라 부른다.

그래프가 입력으로 주어졌을 때, 이 그래프가 이분 그래프인지 아닌지 판별하는 프로그램을 작성하시오.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1707">https://www.acmicpc.net/problem/1707
</a>

---
## 입력
입력은 여러 개의 테스트 케이스로 구성되어 있는데, 첫째 줄에 테스트 케이스의 개수 K가 주어진다. 각 테스트 케이스의 첫째 줄에는 그래프의 정점의 개수 V와 간선의 개수 E가 빈 칸을 사이에 두고 순서대로 주어진다. 각 정점에는 1부터 V까지 차례로 번호가 붙어 있다. 이어서 둘째 줄부터 E개의 줄에 걸쳐 간선에 대한 정보가 주어지는데, 각 줄에 인접한 두 정점의 번호 u, v (u ≠ v)가 빈 칸을 사이에 두고 주어진다. 

---
## 출력
K개의 줄에 걸쳐 입력으로 주어진 그래프가 이분 그래프이면 YES, 아니면 NO를 순서대로 출력한다.

---
## 제한
- 2 ≤ K ≤ 5
- 1 ≤ V ≤ 20,000
- 1 ≤ E ≤ 200,000

---
## 예제 입력 1

```
입력
2
3 2
1 3
2 3
4 4
1 2
2 3
3 4
4 2

출력
YES
NO
```
---

## 풀이 방식
- 이분 그래프는 같은 집합에 속한 정점끼리는 서로 연결된 간선이 없다는 특징이 있다.
- 색깔로 구분하여 빨간색이 방문한 정점은 파란색으로 체크, 파란색으로 방문한 정점은 반대로 빨간색으로 체크하여 마지막에 같은색끼리 이어진 간선이 있는지 체크하면 이분 그래프인지 아닌지 판단할 수 있다.
- 0 : 방문 안함
- 1 : 방문함, 빨간색
- 2 : 방문함, 파란색

---

## 풀이 방식 코드
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
