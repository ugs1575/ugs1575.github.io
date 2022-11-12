---
layout: default
title: BOJ 2004_조합 0의 개수
parent: Algorithms
last_modified_at: "22.11.05"
---

# [백준] 2004번 조합 0의 개수
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
$n \choose m$의 끝자리 $0$의 개수를 출력하는 프로그램을 작성하시오.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1676">https://www.acmicpc.net/problem/1676
</a>

---
## 입력
첫째 줄에 N이 주어진다. (0 ≤ N ≤ 500)

---
## 출력
첫째 줄에 구한 0의 개수를 출력한다.

---
## 예제 입력 1

```
입력
10

출력
2
```

## 예제 입력 2

```
입력
3

출력
0
```

---
## 풀이 방식

- $\frac{n!}{m!(n-m)!}$
- 2x5 = 10, N!를 소인수 분해 했을 때 2x5 조합이 몇개 나오는지 알면된다.
- 2와 5의 개수를 같이 세어야 한다.

---

## 풀이 방식 코드
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int ans = 0;

        for (int i = 5; i < n; i*=5) {
            ans += n/i;
        }

        System.out.println(ans);
    }
}
```
