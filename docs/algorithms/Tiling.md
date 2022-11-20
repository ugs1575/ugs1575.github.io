---
layout: default
title: BOJ 11726_2xn 타일링
parent: Algorithms
last_modified_at: "22.08.29"
---

# [백준] 11726번 2xn 타일링
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
<a href="https://www.acmicpc.net/problem/11726">https://www.acmicpc.net/problem/11726
</a>

---
## 풀이 방식
- d[n] = 2xn 면적에 타일을 채우는 방법의 수
1. 마지막에 2x1 타일 한 개 붙이기
2. 1x2타일 2개를 위 아래로 겹쳐서 붙이기
    - 왜냐하면 항상 1x2을 하나 붙이게 되면 무조건 1x2를 겹쳐서 붙여야 면적을 채울 수 있기 때문이다.

2가지 방법을 생각하면 된다.
<br>
- 1x2 타일을 붙이면 가로 면적이 1만큼 줄고 결국 2x(n-1) 면적을 채우는 방법의 수를 구해야 한다.<br>
- 2x1 타일을 붙이면 가로 면적이 2만큼 줄고 결국 2x(n-2) 면적을 채우는 방법의 수를 구해야 한다.<br>

경우의 수를 구하는 것이기 때문에 두 가지 방법을 더해주면 된다.

- 가장 중요한 점은 d[0] 즉, 2x0 면적에 타일을 채우는 방법의 수를 1이라고 생각해야 한다는 것이다.<br>
이렇게 생각하기 쉽지 않은데, 항상 모든 면적이 2x0에서부터 시작한다고 생각하면 d[0] = 1이라고 생각할 수 있다.<br>
- 예를 들어 2x0 면적에서 2x1을 붙이면 면적은 2x1이 된다. 또 2x1을 붙이면 2x2가 된다.

그리고 문제에서 10007로 나눈 나머지 값을 출력하라고 했으니 d[n]에 10007로 나눈 나머지를 저장해 주면 된다.

---

## Top-Down 방식
```java
import java.util.Scanner;

public class Main {
   public  static int[] d;
   public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        d = new int[n+1];
        d[0] = 1;
        d[1] = 1;
        System.out.println(tiling(n));
    }

    private static int tiling(int n) {
        if (d[n] > 0) return d[n];

        d[n] = tiling(n-1) + tiling(n-2);
        d[n] = d[n]%10007;

        return d[n];
    }
}

```
## Bottom-up 방식
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] d = new int[n+1];
        d[0] = 1;
        d[1] = 1;

        for (int i = 2; i <= n; i++) {
            d[i] = d[i-1] + d[i-2];
            d[i] = d[i]%10007;
        }
        System.out.println(d[n]);
    }
}
```