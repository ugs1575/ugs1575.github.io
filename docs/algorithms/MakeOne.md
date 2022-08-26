---
layout: default
title: BOJ 1463_1로 만들기
parent: Algorithms
last_modified_at: "22.08.26"
---

# [백준] 1463번 1로 만들기
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
정수 X에 사용할 수 있는 연산은 다음과 같이 세 가지 이다.

1. X가 3으로 나누어 떨어지면, 3으로 나눈다.
2. X가 2로 나누어 떨어지면, 2로 나눈다.
3. 1을 뺀다.

정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1463">https://www.acmicpc.net/problem/1463
</a>

---
## 입력
<br>
첫째 줄에 1보다 크거나 같고, 106보다 작거나 같은 정수 N이 주어진다.

---
## 출력
<br>
첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

---
## 예제 입력 1

```
입력
2

출력
1
```
## 예제 입력 2
```
입력
10

출력
3
```
---
## 접근 방식
<br>
한번에 풀었다 ㅎㅅㅎ<br>
다만 memoization을 하지 않아 이 이부분이 들어가면 더 좋을 것 같다.

---
## 풀이 방식
<br>
세가지 연산을 모두 다 해보지만<br>
작은 수일 때 연산하는 최솟값을 저장해놓으면 큰수를 구할 수 있다.<br>
d[x] = x가 1이 되는 최소 연산 횟수


---

## 내가 푼 코드
```java
import java.util.Scanner;

public class Main {
    static int ans = Integer.MAX_VALUE;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();
        makeOne(x, 0);
        System.out.println(ans);
    }

    private static void makeOne(int x, int count) {
        if (x <= 0 || count > ans) {
            return;
        }

        if (x == 1) {
            ans = Math.min(count, ans);
            return;
        }

        if (x % 3 == 0) {
            makeOne(x/3, count+1);
        }

        if (x % 2 == 0) {
            makeOne(x/2, count+1);
        }

        makeOne(x-1, count+1);
    }
}
```