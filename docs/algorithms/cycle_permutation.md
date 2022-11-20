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
## 문제
1부터 N까지 정수 N개로 이루어진 순열을 나타내는 방법은 여러 가지가 있다. 예를 들어, 8개의 수로 이루어진 순열 (3, 2, 7, 8, 1, 4, 5, 6)을 배열을 이용해 표현하면  
 \(\begin{pmatrix} 1 & 2 &3&4&5&6&7&8 \\  3& 2&7&8&1&4&5&6 \end{pmatrix}\) 와 같다. 또는, Figure 1과 같이 방향 그래프로 나타낼 수도 있다.
<p align="center" display="inline-block"><img src="https://www.acmicpc.net/upload/images2/permut.png"></p>

순열을 배열을 이용해  
 \(\begin{pmatrix} 1 & \dots & i & \dots &n \\  \pi_1& \dots& \pi_i & \dots & \pi_n \end{pmatrix}\) 로 나타냈다면, i에서 πi로 간선을 이어 그래프로 만들 수 있다.

Figure 1에 나와있는 것 처럼, 순열 그래프 (3, 2, 7, 8, 1, 4, 5, 6) 에는 총 3개의 사이클이 있다. 이러한 사이클을 "순열 사이클" 이라고 한다.

N개의 정수로 이루어진 순열이 주어졌을 때, 순열 사이클의 개수를 구하는 프로그램을 작성하시오.



- 문제링크 :
<a href="https://www.acmicpc.net/problem/10451">https://www.acmicpc.net/problem/10451
</a>

---
## 입력
첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스의 첫째 줄에는 순열의 크기 N (2 ≤ N ≤ 1,000)이 주어진다. 둘째 줄에는 순열이 주어지며, 각 정수는 공백으로 구분되어 있다.

---
## 출력
각 테스트 케이스마다, 입력으로 주어진 순열에 존재하는 순열 사이클의 개수를 출력한다.

---
## 예제 입력 1

```
입력
2
8
3 2 7 8 1 4 5 6
10
2 1 3 4 5 6 7 9 10 8

출력
3
7
```
---

## 풀이 방식
- 순열이어서 무조건 싸이클이 있을 수 밖에 없다.
- 그래서 방문했던 점을 방문했는지 검사할 필요가 없고 그냥 탐색이 끊어지면 +1 해주면 된다.

---

## 풀이 방식 코드
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
