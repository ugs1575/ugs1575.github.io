---
layout: default
title: BOJ 9466_텀 프로젝트
parent: Algorithms
last_modified_at: "22.11.28"
---

# [백준] 9466번 텀 프로젝트
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
<a href="https://www.acmicpc.net/problem/9466">https://www.acmicpc.net/problem/9466
</a>

---
## 풀이방식
- 단순히 사이클을 찾는 문제와 다르다.
- 사이클을 찾을 때 방문했던 점을 다시 방문했다고 하면 사이클이었지만 이 문제는 사이클이 아닐 수 있다.
- 방문을 체크할 때 그룹을 나누어서 같은 그룹에 속하면서 방문했던 점을 방문했는지를 같이 체크해주어야한다.
- step이라는 배열을 따로 두어 해당 정점이 몇번째인지를 저장해두었다가 방문했던 점을 다시 방문했을 때 현재 step-방문한 점의 step 을 계산해주면 사이클에 속한 개수를 구할 수 있다.

---

## 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        for (int i = 0; i < t; i++) {
            int n = sc.nextInt();
            int[] graph = new int[n + 1];
            int[] visit = new int[n + 1];
            int[] step = new int[n + 1];

            for (int j = 1; j <= n; j++) {
                graph[j] = sc.nextInt();
            }

            int result = 0;
            for (int j = 1; j <= n; j++) {
                if (visit[j] != 0) continue;
                result += dfs(graph, visit, step, 1, j, j);
            }

            System.out.println(n-result);
        }
    }

    private static int dfs(int[] graph, int[] visit, int[] step, int length, int start, int x) {
        if (visit[x] != 0) {
            if (start == step[x]) {
                return length-visit[x];
            }

            return 0;
        }

        visit[x] = length;
        step[x] = start;
        length++;
        return dfs(graph, visit, step, length, start, graph[x]);
    }
}

```
