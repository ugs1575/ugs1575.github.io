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
## 문제
수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/11053">https://www.acmicpc.net/problem/11053
</a>

---
## 입력
첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)


---
## 출력
첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.

---
## 예제 입력 1

```
입력
6
10 20 10 30 20 50

출력
4
```

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


