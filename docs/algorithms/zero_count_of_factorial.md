---
layout: default
title: BOJ 1676_팩토리얼 0의 개수
parent: Algorithms
last_modified_at: "22.11.05"
---

# [백준] 1676번 팩토리얼 0의 개수
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
N!에서 뒤에서부터 처음 0이 아닌 숫자가 나올 때까지 0의 개수를 구하는 프로그램을 작성하시오.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1676">https://www.acmicpc.net/problem/1676
</a>

---
## 입력
첫째 줄에 N이 주어진다. (0 ≤ N ≤ 500)

---
## 출력
<br>
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
<br>

- 10! = 3628800이다.
- 10!를 소인수분해 해보면
- 10! = 1 x 2 x 3 x 4($2^2$) x 5 x 6 x 7 x 8($2^3$) x 9($3^2$) x 10($2x5$)
- 2x5 = 10, N!를 소인수 분해 했을 때 2x5 조합이 몇개 나오는지 알면된다.
- 5의 개수가 항상 2의 개수보다 적기 때문에 5의 개수만 세어주면 된다.
- N! 0의 개수 = n/5 + n/$5^2$ + ....
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
