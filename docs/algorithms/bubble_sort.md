---
layout: default
title: BOJ 1377_버블 소트
parent: Algorithms
last_modified_at: "22.11.12"
---

# [백준] 1377번 버블 소트
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
버블 소트 알고리즘을 다음과 같이 C++로 작성했다.
```c++
bool changed = false;
for (int i=1; i<=N+1; i++) {
    changed = false;
    for (int j=1; j<=N-i; j++) {
        if (A[j] > A[j+1]) {
            changed = true;
            swap(A[j], A[j+1]);
        }
    }
    if (changed == false) {
        cout << i << '\n';
        break;
    }
}
```
위 소스에서 N은 배열의 크기이고, A는 정렬해야 하는 배열이다. 배열은 A[1]부터 사용한다.

위와 같은 소스를 실행시켰을 때, 어떤 값이 출력되는지 구해보자.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1377">https://www.acmicpc.net/problem/1377
</a>

---
## 입력
첫째 줄에 N이 주어진다. N은 500,000보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에 A[1]부터 A[N]까지 하나씩 주어진다. A에 들어있는 수는 1,000,000보다 작거나 같은 자연수 또는 0이다.

---
## 출력
정답을 출력한다.

---
## 예제 입력 1

```
입력
5
10
1
5
2
3

출력
3
```

## 예제 입력 2

```
입력
5
1
3
5
7
9

출력
1
```

---
## 풀이 방식
- 버블 소트가 총 몇단계로 이뤄지는지 구하는 문제다.
- 뒤로 이동한 1단계만에 바로 뒤로 이동할 수 있지만 앞으로 이동한 숫자들은 단계마다 한개씩 이동한다.
- 입력으로 주어진 숫자의 인덱스를 저장했다가, 정렬이 끝난 숫자의 인덱스를 비교해서 앞으로 이동한 숫자들 중 최대값을 출력하면 된다.

---

## 풀이 방식 코드
```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;

class Pair implements Comparable<Pair>{
    int index;
    int number;

    public Pair(int index, int number) {
        this.index = index;
        this.number = number;
    }


    @Override
    public int compareTo(Pair o) {
        if (this.number < o.number) {
            return -1;
        } else if (this.number == o.number) {
            return 0;
        } else {
            return 1;
        }
    }
}

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        ArrayList<Pair> numbers = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            numbers.add(new Pair(i, Integer.parseInt(br.readLine())));
        }

        Collections.sort(numbers);

        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int max = 0;
        for (int i = 0; i < n; i++) {
            int diff = numbers.get(i).index - i;
            if (diff > 0 && diff > max) {
                max = diff;
            }
        }

        bw.write(max+1+"\n");
        bw.flush();
        bw.close();

    }
}
```
