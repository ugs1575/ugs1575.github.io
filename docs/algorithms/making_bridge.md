---
layout: default
title: BOJ 2146_다리 만들기
parent: Algorithms
last_modified_at: "22.11.20"
---

# [백준] 2146번 다리 만들기
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
<a href="https://www.acmicpc.net/problem/2146">https://www.acmicpc.net/problem/2146
</a>

---
## 풀이방식
### 내가 푼 방식
1. 그룹을 나눈다.
2. 각각의 섬에서 bfs를 통해 길이를 기록하고 다른 섬을 만났을 때 마다 가장 짧은 다리길이를 update 해준다.

### 더 빠른 방법
1. 그룹을 기록할 배열을 하나 만든다.
2. 거리를 기록할 배열을 만들고 섬에는 0을 넣어준다. 나머지는 -1
3. 그룹도 각각 확장하고 섬거리도 확장한다.
4. 그룹 배열을 조사하며 인접한 배열에 다른 그룹이 있는 곳에 다리를 만들 수 있고, 그 거리는 거리 배열을 보면 된다. 각각 해당되는 위치를 거리배열에서 값을 더해주면 된다.

---

## 더 빠른 방법 코드
```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

class Pair {
    int x;
    int y;

    public Pair(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Main {
    static int n;
    static int[][] graph;
    static int[][] island;
    static int[][] distance;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, 1, -1};
    static int min;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        n = sc.nextInt();
        min = n*n;
        graph = new int[n][n];
        island = new int[n][n];
        distance = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                graph[i][j] = sc.nextInt();
            }
        }

        //1.그룹을 만든다 하나의 배열에
        int groupCount = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (graph[i][j] == 1 && island[i][j] == 0) {
                    groupCount += 1;
                    findIsland(i, j, groupCount);
                }
            }
        }

        //2.거리 배열을 만들고 섬에는 0을 넣어준다. 나머지는 -1
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (island[i][j] == 0) {
                    distance[i][j] = -1;
                }
            }
        }

        //그룹도 각각 확장하고 섬거리도 확장한다.
        Queue<Pair> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (island[i][j] != 0) {
                    q.add(new Pair(i, j));
                }
            }
        }
        bfsIsland(q);

        q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (distance[i][j] == 0) {
                    q.add(new Pair(i, j));
                }
            }
        }
        bfsDistance(q);

        //그룹배열을 조사하며 인접한 배열에 다른 그룹이 있는 곳에 다리를 만들 수 있고
        //그 거리는 거리 배열을 보면 된다. 각각 해당되는 위치를 거리배열에서 값을 더해주면 된다.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 0; k < 4; k++) {
                    int nx = i + dx[k];
                    int ny = j + dy[k];

                    if (nx < 0 || nx >= n || ny < 0 || ny >= n) continue;
                    if (island[i][j] != island[nx][ny]) {
                        min = Math.min(min, distance[i][j] + distance[nx][ny]);
                    }
                }
            }
        }

        System.out.println(min);
    }
    
    private static void bfsDistance(Queue<Pair> q) {
        while (!q.isEmpty()) {
            Pair current = q.remove();
            for (int i = 0; i < 4; i++) {
                int nx = current.x + dx[i];
                int ny = current.y + dy[i];

                if (nx < 0 || nx >= n || ny < 0 || ny >= n) continue;
                if (distance[nx][ny] != -1) continue;

                q.add(new Pair(nx, ny));
                distance[nx][ny] = distance[current.x][current.y] + 1;
            }
        }
    }

    private static void bfsIsland(Queue<Pair> q) {
        while (!q.isEmpty()) {
            Pair current = q.remove();
            for (int i = 0; i < 4; i++) {
                int nx = current.x + dx[i];
                int ny = current.y + dy[i];

                if (nx < 0 || nx >= n || ny < 0 || ny >= n) continue;
                if (island[nx][ny] != 0) continue;

                q.add(new Pair(nx, ny));
                island[nx][ny] = island[current.x][current.y];
            }
        }
    }

    private static void findIsland(int x, int y, int groupCount) {
        Queue<Pair> q = new LinkedList<>();
        island[x][y] = groupCount;
        q.add(new Pair(x, y));

        while (!q.isEmpty()) {
            Pair current = q.remove();
            for (int i = 0; i < 4; i++) {
                int nx = current.x + dx[i];
                int ny = current.y + dy[i];

                if (nx < 0 || nx >= n || ny < 0 || ny >= n) continue;
                if (graph[nx][ny] == 0) continue;
                if (island[nx][ny] != 0) continue;

                q.add(new Pair(nx, ny));
                island[nx][ny] = groupCount;
            }
        }
    }
}
```
