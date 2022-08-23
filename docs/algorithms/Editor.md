---
layout: default
title: BOJ 1406_에디터
parent: Algorithms
last_modified_at: "22.08.23"
---

# [백준] 1406번 쇠막대기
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
한 줄로 된 간단한 에디터를 구현하려고 한다. 이 편집기는 영어 소문자만을 기록할 수 있는 편집기로, 최대 600,000글자까지 입력할 수 있다.

이 편집기에는 '커서'라는 것이 있는데, 커서는 문장의 맨 앞(첫 번째 문자의 왼쪽), 문장의 맨 뒤(마지막 문자의 오른쪽), 또는 문장 중간 임의의 곳(모든 연속된 두 문자 사이)에 위치할 수 있다. 즉 길이가 L인 문자열이 현재 편집기에 입력되어 있으면, 커서가 위치할 수 있는 곳은 L+1가지 경우가 있다.

이 편집기가 지원하는 명령어는 다음과 같다.

<table>
    <tbody>
        <tr>
            <td>L</td>
            <td>커서를 왼쪽으로 한 칸 옮김 (커서가 문장의 맨 앞이면 무시됨)</td>
        </tr>
        <tr>
            <td>D</td>
            <td>커서를 오른쪽으로 한 칸 옮김 (커서가 문장의 맨 뒤이면 무시됨)</td>
        </tr>
        <tr>
            <td>B</td>
            <td>커서 왼쪽에 있는 문자를 삭제함 (커서가 문장의 맨 앞이면 무시됨)
            <br>
            삭제로 인해 커서는 한 칸 왼쪽으로 이동한 것처럼 나타나지만, 실제로 커서의 오른쪽에 있던 문자는 그대로임
            </td>
        </tr>
        <tr>
            <td>P $</td>
            <td>$라는 문자를 커서 왼쪽에 추가함
            </td>
        </tr>
    </tbody>
</table>

초기에 편집기에 입력되어 있는 문자열이 주어지고, 그 이후 입력한 명령어가 차례로 주어졌을 때, 모든 명령어를 수행하고 난 후 편집기에 입력되어 있는 문자열을 구하는 프로그램을 작성하시오. 단, 명령어가 수행되기 전에 커서는 문장의 맨 뒤에 위치하고 있다고 한다.

- 문제링크 :
<a href="https://www.acmicpc.net/problem/1406">https://www.acmicpc.net/problem/1406
</a>

---
## 입력
<br>
첫째 줄에는 초기에 편집기에 입력되어 있는 문자열이 주어진다. 이 문자열은 길이가 N이고, 영어 소문자로만 이루어져 있으며, 길이는 100,000을 넘지 않는다. 둘째 줄에는 입력할 명령어의 개수를 나타내는 정수 M(1 ≤ M ≤ 500,000)이 주어진다. 셋째 줄부터 M개의 줄에 걸쳐 입력할 명령어가 순서대로 주어진다. 명령어는 위의 네 가지 중 하나의 형태로만 주어진다. 

---
## 출력
<br>
첫째 줄에 모든 명령어를 수행하고 난 후 편집기에 입력되어 있는 문자열을 출력한다.

---
## 예제 입력 1

```
입력
abcd
3
P x
L
P y

출력
17
```
## 예제 입력 2
```
입력
abc
9
L
L
L
L
L
P x
L
B
P y

출력
yxabc
```
## 예제 입력 3
```
입력
dmih
11
B
B
P x
L
B
B
B
P y
D
D
P z

출력
yxz
```
---
## 접근 방식
<br>
한번에 풀었다 ㅎㅅㅎ<br>
첨에는 시간초과가 났긴 했는데 입출력을 BufferedReader로 바꿨더니 해결되었다<br>
출력할때 왼쪽 스택에 있는 문자들을 먼저 붙이고, 그 다음 오른쪽 스택을 돌면서 문자를 만들었는데, 그냥 왼쪽 스택을 하나씩 꺼내서 오른쪽 스택에 넣고 한번에 반환값을 만드는게 더 나은 것 같다.

---
## 풀이 방식
<br>

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