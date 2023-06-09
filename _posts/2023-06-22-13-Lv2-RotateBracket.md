---
title: Lv2 - 괄호 회전하기, Java
author: park
date: 2023-06-22 11:06:00 +0800
categories: [알고리즘, 월간 코드 챌린지 시즌2]
tags: [typography]
math: true
mermaid: true
published: true # 포스팅 개시할 때, 바로 반영되는 옵션
# image: 
#   path: /assets/img/03.Algorithm/05.Lv1-SecretMap/01.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---

### 소제목 목록
● 문제<br/>
● 소감<br/>
● 해결 코드<br/>
<br/>

<i>출처: https://school.programmers.co.kr/learn/courses/30/lessons/76502</i><br/>
<br/>

---

### ● 문제

다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.<br/>
<br/>
이번 문제는 대괄호가 들어가면 에러가 발생하는 Markdown 파일의 고질적인 문제로 설명을 따로 기입하지 않겠습니다.<br/>
문제는 출처란의 URL을 통해 확인해주세요.<br/>

---

### ● 소감

문제를 보면 이전에 풀었던 문제의 응용이라는 것을 알수 있다.<br/>
<br/>
저장된 가장 마지막 괄호가 현재 비교하는 괄호와 짝이 맞으면 제거하기,<br/>
즉 Stack 을 사용했던 문제와 결이 비슷했다.<br/>
<br/>
물론 해결 방식에서 성능이 더 좋은 방법이 있을텐데, 그것은 알아봐야겠다.<br/>
<br/>

---

### ● 해결 코드

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Stack;

public class Solution {
    Map<Character, Character> friendBracket;

    public int solution(String s) {
        int answer = 0;
        
        this.initFriendBracket();
        
        Stack<Character> stack;
        
        int sLength = s.length();
        
        for (int i = 0; i < sLength; i++) {
            stack = new Stack<>();

            for (int j = 0; j < sLength; j++) {
                char ch = s.charAt(j);
                
                if (!stack.isEmpty() && (stack.peek() == friendBracket.get(ch))) {
                    stack.pop();
                } else {
                    stack.push(ch);
                }
            }

            if (stack.isEmpty()) {
                answer++;
            }
            
            s = s.substring(1, (sLength)) + s.charAt(0);
        }
        
        return answer;
    }
    
    public void initFriendBracket() {
        friendBracket = new HashMap<>();
        friendBracket.put('역소괄호', '정소괄호');
        friendBracket.put('역중괄호', '정중괄호');
        friendBracket.put('역대괄호', '정대괄호');
    }
}
```