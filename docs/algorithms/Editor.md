---
layout: default
title: BOJ 1406_에디터
parent: Algorithms
last_modified_at: "22.08.23"
---

# [백준] 1406번 에디터
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
<a href="https://www.acmicpc.net/problem/1406">https://www.acmicpc.net/problem/1406
</a>

---
## 접근 방식
한번에 풀었다 ㅎㅅㅎ<br>
첨에는 시간초과가 났긴 했는데 입출력을 BufferedReader로 바꿨더니 해결되었다<br>
출력할때 왼쪽 스택에 있는 문자들을 먼저 붙이고, 그 다음 오른쪽 스택을 돌면서 문자를 만들었는데, 그냥 왼쪽 스택을 하나씩 꺼내서 오른쪽 스택에 넣고 한번에 반환값을 만드는게 더 나은 것 같다.

---
## 풀이 방식
1. 스택을 2개를 사용한다. 
- L : 왼쪽 스택 pop한 값을 오른쪽 스택에 넣는다.
- D : 오른쪽 스택 pop한 값을 왼쪽 스택에 넣는다.
- B : 왼쪽 스택 pop
- P x : 왼쪽 스택에 x를 push
2. 출력은 왼쪽 스택 값들은 앞에서부터 값을 붙이고 오른쪽 스택값들은 뒤로(정상적으로) 붙인다.


---
## 코드
```java
import java.io.*;
import java.util.Stack;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();
        int n = Integer.parseInt(br.readLine());
        Stack<Character> left = new Stack<>();
        Stack<Character> right = new Stack<>();

        for (int i = 0; i < s.length(); i++) {
            left.push(s.charAt(i));
        }

        for (int i = 0; i < n; i++) {
            String command = br.readLine();
            char first = command.charAt(0);

            if (first == 'L' && !left.empty()) {
                right.push(left.pop());
            } else if (first == 'D' && !right.empty()) {
                left.push(right.pop());
            } else if (first == 'B' && !left.empty()) {
                left.pop();
            } else if (first == 'P') {
                left.push(command.charAt(2));
            }
        }

        while (!left.empty()) {
            right.push(left.pop());
        }

        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        while(!right.empty()){
            bw.write(Character.toString(right.pop()));
        }
        bw.flush();
        bw.close();
    }
}
```