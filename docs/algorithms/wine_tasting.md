---
layout: default
title: BOJ 2156_포도주 시식
parent: Algorithms
last_modified_at: "22.09.13"
---

# [백준] 2156번 포도주 시식
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
효주는 포도주 시식회에 갔다. 그 곳에 갔더니, 테이블 위에 다양한 포도주가 들어있는 포도주 잔이 일렬로 놓여 있었다. 효주는 포도주 시식을 하려고 하는데, 여기에는 다음과 같은 두 가지 규칙이 있다.

포도주 잔을 선택하면 그 잔에 들어있는 포도주는 모두 마셔야 하고, 마신 후에는 원래 위치에 다시 놓아야 한다.
연속으로 놓여 있는 3잔을 모두 마실 수는 없다.
효주는 될 수 있는 대로 많은 양의 포도주를 맛보기 위해서 어떤 포도주 잔을 선택해야 할지 고민하고 있다. 1부터 n까지의 번호가 붙어 있는 n개의 포도주 잔이 순서대로 테이블 위에 놓여 있고, 각 포도주 잔에 들어있는 포도주의 양이 주어졌을 때, 효주를 도와 가장 많은 양의 포도주를 마실 수 있도록 하는 프로그램을 작성하시오. 

예를 들어 6개의 포도주 잔이 있고, 각각의 잔에 순서대로 6, 10, 13, 9, 8, 1 만큼의 포도주가 들어 있을 때, 첫 번째, 두 번째, 네 번째, 다섯 번째 포도주 잔을 선택하면 총 포도주 양이 33으로 최대로 마실 수 있다.


- 문제링크 :
<a href="https://www.acmicpc.net/problem/2156">https://www.acmicpc.net/problem/2156
</a>

---
## 입력
첫째 줄에 포도주 잔의 개수 n이 주어진다. (1 ≤ n ≤ 10,000) 둘째 줄부터 n+1번째 줄까지 포도주 잔에 들어있는 포도주의 양이 순서대로 주어진다. 포도주의 양은 1,000 이하의 음이 아닌 정수이다.

---
## 출력
첫째 줄에 최대로 마실 수 있는 포도주의 양을 출력한다.

---
## 예제 입력 1

```
입력
6
6
10
13
9
8
1

출력
33
```

---
## 접근 방식
d[i] = 1번째 ~ i번째까지 와인을 마셨을 때 최댓값이라고 정의했을 때<br>
i번째를 마시는 경우, 마시지 않는 경우 2가지 방식을 이차원 배열로 풀려고 하니까<br>
연속을 처리하는 부분해서 풀리지 않았다.<br>

---

## 풀이 방식 1 (이차원 배열 사용)
- d[i][j] = 1번부터 i까지 포도주가 있을 떼 i번째 잔이 연속 j번일때 최댓값
- 0번 연속 : d[n][0] = max(d[n-1][0], d[n-1][1], d[n-1][2])
  - 0번 연속이라는 것은 n번째 잔을 마시지 않았을 경우를 의미한다.
  - 그렇다면 n-1번째 잔을 마시지 않거나, 1번째 연속이거나 2번째 연속해서 마셨거나 3가지 경우 모두 가능하다.
- 1번 연속 : d[n][1] = d[n-1][0] + wine[n]
  - 1번 연속했다는 건 n번째 잔을 마시고 n-1번째 잔은 마시지 않은 것을 의미한다.
- 2번 연속 : d[n][2] = d[n-1][1] + wine[n]
  - 2번 연속했다는 건 n번째 잔을 마시고 n-1번째 잔도 마신 것을 의미한다.
- 3가지 경우를 모두 구해 가장 최댓값을 반환하면 된다.


## 풀이 방식1 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] wine = new int[n + 1];
        int[][] d = new int[n + 1][3];

        for (int i = 1; i <= n; i++) {
            wine[i] = sc.nextInt();
        }

        for (int i = 1; i <= n; i++) {
            d[i][0] = Math.max(Math.max(d[i - 1][0], d[i - 1][1]), d[i - 1][2]);
            d[i][1] = d[i - 1][0] + wine[i];
            d[i][2] = d[i - 1][1] + wine[i];
        }

        System.out.println(Math.max(Math.max(d[n][0], d[n][1]), d[n][2]));
    }
}
```

---

## 풀이 방식 2 (일차원 배열 사용)
- d[n] = 1번째 부터 n번째까지 포도주를 마셨을 때 마실 수 잇는 포도주의 최대양
- 0번 연속 : d[n-1]
- 1번 연속 
  - n번째가 1번 연속이라는 것은 n번째는 마시고 n-1은 마시지 않았다.
  - n-2번째는 마셨거나 마시지 않았어도 상관없다.
  - d[n-2] + wine[n]
- 2번 연속
  - n번째가 2번 연속이라는 것은 n번째와 n-1번째를 마셨다.
  - n-2번째는 마시지 않았어야 한다.
  - n-3번째는 마셨거나 마시지 않았어도 상관없다.
  - d[n-3] + wine[n] + wine[n-1]


## 풀이 방식2 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] wine = new int[10001];
        int[] d = new int[10001];

        for (int i = 1; i <= n; i++) {
            wine[i] = sc.nextInt();
        }

        d[1] = wine[1];
        d[2] = wine[1] + wine[2];

        for (int i = 3; i <= n; i++) {
            int zero = d[i - 1];
            int once = d[i - 2] + wine[i];
            int twice = d[i - 3] + wine[i] + wine[i - 1];
            d[i] = Math.max(Math.max(zero, once), twice);
        }

        System.out.println(d[n]);
    }
}


```