---
layout: default
title: BOJ 6064_카잉 달력
parent: Algorithms
last_modified_at: "22.11.20"
---

# [백준] 6064번 카잉 달력
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
<a href="https://www.acmicpc.net/problem/6064">https://www.acmicpc.net/problem/6064
</a>

---
## 풀이방식
- m과 n의 최댓값이 40,000로 최대 mxn 이라 생각하면 시간 초과가 난다.
- m과 n 중 한가지에 해당되는 것만 검사해서 시간을 줄일 수 있다.
- 처음에는 왜 x,y에 -1을 해주는 지 이해가 안됐다. 나머지 연산으로 계산 문제를 풀게 되면 나머지가 0이 나오는 순간 때문이다.
- 예를 들면 m n x y 가 차례대로 12 12 12 12 라고 한다면 나머지 연산으로 풀었을 때  12 % 12 = 0 이 되기 때문에 예외처리를 해야한다.

---

## 코드
```java
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int t = sc.nextInt();

		for (int i = 0; i < t; i++) {
			int m = sc.nextInt();
			int n = sc.nextInt();
			int x = sc.nextInt() - 1;
			int y = sc.nextInt() - 1;

			int result = -1;
			for (int j = x; j < m * n; j += m) {
				if (j % n == y) {
					result = j + 1;
					break;
				}
			}

			System.out.println(result);
		}
	}
}
```
