---
layout: default
title: BOJ 10799_쇠막대기
parent: Algorithms
last_modified_at: "22.08.22"
---

# [백준] 10799번 쇠막대기
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
<a href="https://www.acmicpc.net/problem/10799">https://www.acmicpc.net/problem/10799
</a>

---
## 접근 방식
정답률이 높은 문제였는데, 매번 오랜만에 시도할 때마다 풀지 못했다.
고민하다가 생각한 방식 다음과 같다.
1. 레이저인 괄호의 인덱스를 저장해놓고
2. 입력 문자를 한 글자씩 돌면서
    - 만약, 레이저 인덱스이면 건너뛴다.
    - 여는 괄호이면 해당 인덱스를 스택에 넣는다.
    - 닫는 괄호이면 스택에서 pop 한다. pop 한 값이 여는 괄호이면 저장한 레이저 인덱스를 돌면서 여는 괄호와 닫는 괄호의 인덱스에 속한 레이저 총 수를 찾는다.
찾은 총개수에 +1을 하여 반환할 변수에 더한다.

이 접근 방식이 시간 초과가 날 걸 알면서도 풀었지만 역시나 시간 초과

---
## 풀이 방식
풀이 방식을 보니 입력 문자를 한 글자씩 돌면서 
1. 여는 괄호이면 stack에 인덱스를 push
2. 닫는 괄호이면 stack에 pop 한 값과 인덱스가 1차이가 난다면 => 레이저다
그때 여는 괄호의 수를 세어주면 된다. 즉, 반환 변수에 스택 사이즈를 더해준다.
3. 닫는 괄호이면서 stack에 pop 한 값과 인덱스가 1차이가 나지 않는다면
+1을 해준다.

결론: 하나의 쇠막대기가 끝나는 지점까지 여는 괄호를 구하면 해당 막대를 통과하는 레이저의 수를 구할 수 있고, 쇠막대기 조각의 총개수는 지나간 레이저의 수 +1이다. 그러니 쇠막대기가 끝나는 시점에서 +1을 해준다. 

---
## 코드
```java
import java.util.*;
public class Main{
    public static void main(String args[]){
        Scanner sc = new Scanner(System.in);
        String input = sc.next();
        int n = input.length();
        int i = 0;
        int stick = 0;

        Stack<Integer> stack = new Stack<Integer>();
        while (i < n){
            if(input.charAt(i) == '('){
                stack.push(i);
            }else{
                //레이저
                if(i-stack.pop()==1){
                    stick+=stack.size();
                    //쇠막대기
                }else{
                    stick++;
                }
            }
            i++;
        }

        System.out.print(stick);

    }
}
```