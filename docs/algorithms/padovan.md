---
layout: default
title: BOJ 9561_파도반수열
parent: Algorithms
last_modified_at: "22.09.23"
---

# [백준] 9561번 파도반수열
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
<img display="inline-block" src="https://www.acmicpc.net/upload/images/pandovan.png" style="float:right">
오른쪽 그림과 같이 삼각형이 나선 모양으로 놓여져 있다. 첫 삼각형은 정삼각형으로 변의 길이는 1이다. 그 다음에는 다음과 같은 과정으로 정삼각형을 계속 추가한다. 나선에서 가장 긴 변의 길이를 k라 했을 때, 그 변에 길이가 k인 정삼각형을 추가한다.

파도반 수열 P(N)은 나선에 있는 정삼각형의 변의 길이이다. P(1)부터 P(10)까지 첫 10개 숫자는 1, 1, 1, 2, 2, 3, 4, 5, 7, 9이다.

N이 주어졌을 때, P(N)을 구하는 프로그램을 작성하시오.


- 문제링크 :
<a href="https://www.acmicpc.net/problem/9561">https://www.acmicpc.net/problem/9561
</a>

---
## 입력
첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, N이 주어진다. (1 ≤ N ≤ 100)

---
## 출력
각 테스트 케이스마다 P(N)을 출력한다.

---
## 예제 입력

```
입력
2
6
12

출력
3
16
```

---
## 풀이 방식
- 그림을 보면 규칙을 찾을 수 있다.
- d[i] = i번째 변의 길이 
- d[i] = d[i-1] + d[i-5]

---

## 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int tc = sc.nextInt();
        long[] d = new long[101];

        d[1] = 1L;
        d[2] = 1L;
        d[3] = 1L;
        d[4] = 2L;

        for (int i = 0; i < tc; i++) {
            int n = sc.nextInt();

            for (int j = 5; j <= n; j++) {
                d[j] = d[j-1] + d[j-5];
            }

            System.out.println(d[n]);
        }

    }
}
```