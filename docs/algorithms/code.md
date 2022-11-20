---
layout: default
title: BOJ 2011_암호코드
parent: Algorithms
last_modified_at: "22.10.04"
---

# [백준] 2011번 암호코드
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
<a href="https://www.acmicpc.net/problem/2011">https://www.acmicpc.net/problem/2011
</a>

---
## 풀이 방식
- d[i] = i번째 문자까지 해석했을 때, 나올 수 있는 해석의 수
- i번째 문자에서 두가지 경우를 확인할 수 있다.
1. 1자리로 해석되는 경우 (1~9)
2. i-1자리와 함께 2자리로 해석되는 경우 (10~26)
- 따라서 한글자씩 두가지 경우를 검사하면 되는데 2자리로 해석이 안되는 경우는 i-1에 0이 왔을 경우가 있다.
- 1자리로 해석되는 경우의 수는 d[i] = d[i-1] + d[i]
- 2자리로 해석되는 경우의 수는 d[i] = d[i-2] + d[i]가 된다.

---

## 코드
```java
import java.util.Scanner;

public class Main {
    private static long MOD = 1000000L;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        int n = s.length();
        long[] d = new long[n+1];

        s = " " + s;
        d[0] = 1;
        for (int i = 1; i <= n; i++) {
            int x = s.charAt(i) - '0';
            if (x>=1 && x<=9) {
                d[i] += d[i-1];
                d[i] %= MOD;
            }

            if (i == 1) continue;

            int y = s.charAt(i-1) - '0';
            if (y == 0) continue;

            int number = y*10+x;
            if (number>=10 && number<=26) {
                d[i] += d[i-2];
                d[i] %= MOD;
            }
        }

        System.out.println(d[n]);
    }
}
```