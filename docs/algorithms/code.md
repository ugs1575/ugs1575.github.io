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
## 문제
<br>
상근이와 선영이가 다른 사람들이 남매간의 대화를 듣는 것을 방지하기 위해서 대화를 서로 암호화 하기로 했다. 그래서 다음과 같은 대화를 했다.

- 상근: 그냥 간단히 암호화 하자. A를 1이라고 하고, B는 2로, 그리고 Z는 26으로 하는거야.
- 선영: 그럼 안돼. 만약, "BEAN"을 암호화하면 25114가 나오는데, 이걸 다시 글자로 바꾸는 방법은 여러 가지가 있어.
- 상근: 그렇네. 25114를 다시 영어로 바꾸면, "BEAAD", "YAAD", "YAN", "YKD", "BEKD", "BEAN" 총 6가지가 나오는데, BEAN이 맞는 단어라는건 쉽게 알수 있잖아?
- 선영: 예가 적절하지 않았네 ㅠㅠ 만약 내가 500자리 글자를 암호화 했다고 해봐. 그 때는 나올 수 있는 해석이 정말 많은데, 그걸 언제 다해봐?
- 상근: 얼마나 많은데?
- 선영: 구해보자!
어떤 암호가 주어졌을 때, 그 암호의 해석이 몇 가지가 나올 수 있는지 구하는 프로그램을 작성하시오.


- 문제링크 :
<a href="https://www.acmicpc.net/problem/2011">https://www.acmicpc.net/problem/2011
</a>

---
## 입력
<br>
첫째 줄에 5000자리 이하의 암호가 주어진다. 암호는 숫자로 이루어져 있다.

---
## 출력
<br>
나올 수 있는 해석의 가짓수를 구하시오. 정답이 매우 클 수 있으므로, 1000000으로 나눈 나머지를 출력한다.

암호가 잘못되어 암호를 해석할 수 없는 경우에는 0을 출력한다.

---
## 예제 입력 1

```
입력
25114

출력
6
```
## 예제 입력 2

```
입력
1111111111

출력
89
```

---
## 풀이 방식
<br>

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