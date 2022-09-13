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
<br>
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
<br>
첫째 줄에 포도주 잔의 개수 n이 주어진다. (1 ≤ n ≤ 10,000) 둘째 줄부터 n+1번째 줄까지 포도주 잔에 들어있는 포도주의 양이 순서대로 주어진다. 포도주의 양은 1,000 이하의 음이 아닌 정수이다.

---
## 출력
<br>
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
## 풀이 방식 1
<br>
- d[i][j] = 1번부터 i까지 포도주가 있을 떼 i번째 잔이 연속 j번일때 최댓값
- 0번 연속 : d[n][0] = max(d[n-1][0], d[n-1][1], d[n-1][2])
- 1번 연속 : d[n][1] = d[n-1][0] + wine[n]
- 2번 연속 : d[n][2] = d[n-1][1] + wine[n]

---

## 풀이 방식1 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long[][] d = new long[n+1][2];
        d[1][1] = 1L;

        for (int i = 2; i <= n; i++) {
            d[i][0] = d[i-1][1] + d[i-1][0];
            d[i][1] = d[i-1][0];
        }

        long ans = d[n][0] + d[n][1];
        System.out.println(ans);
    }
}
```

## 풀이 방식 2
<br>

- d[n] = n자리 이친수의 갯수
  - d[n]을 구하기 위해서 2가지 방법을 생각해 볼 수 있는데
  1. n자리 이친수 인데 끝에 0이 오는 경우의 수 
  2. 끝에 1이 오는 경우의 수
  - 결국 d[n]을 구하기 위해서는 두가지 경우의 수를 더해주면 된다.

- n자리 이친수 끝에 0이 온다고 한다면 n-1자리에는 0과 1둘다 올 수 있다. 
- 결국 d[n-1]에 0을 붙이는 것과 같다고 볼 수 있다.
- n자리 이친수 끝에 1이 온다고 한다면 n-2자리에 01을 붙이는 것과 같다.
- 결국 d[n-1]에 01을 붙인다고 생각볼 수 있다.

결론적으로 다음과 같이 정의 할 수 있다.
- d[n] = d[n-1] + d[n-2]
---

## 풀이 방식2 코드
```java
import java.util.Scanner;

public class Main {
     public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        long[] d = new long[n+1];

        d[1] = 1L;
        if (n >= 2) {
            d[2] = 1L;
        }
        for (int i = 3; i <= n; i++) {
            d[i] = d[i-1] + d[i-2];
        }

        System.out.println(d[n]);
    }
}


```