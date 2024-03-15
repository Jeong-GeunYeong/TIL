# 둘만의 암호

### 문제 설명
두 문자열 s와 skip, 그리고 자연수 index가 주어질 때, 다음 규칙에 따라 문자열을 만들려 합니다. 암호의 규칙은 다음과 같습니다.

문자열 s의 각 알파벳을 index만큼 뒤의 알파벳으로 바꿔줍니다.
index만큼의 뒤의 알파벳이 z를 넘어갈 경우 다시 a로 돌아갑니다.
skip에 있는 알파벳은 제외하고 건너뜁니다.
예를 들어 s = "aukks", skip = "wbqd", index = 5일 때, a에서 5만큼 뒤에 있는 알파벳은 f지만 [b, c, d, e, f]에서 'b'와 'd'는 skip에 포함되므로 세지 않습니다. 따라서 'b', 'd'를 제외하고 'a'에서 5만큼 뒤에 있는 알파벳은 [c, e, f, g, h] 순서에 의해 'h'가 됩니다. 나머지 "ukks" 또한 위 규칙대로 바꾸면 "appy"가 되며 결과는 "happy"가 됩니다.

두 문자열 s와 skip, 그리고 자연수 index가 매개변수로 주어질 때 위 규칙대로 s를 변환한 결과를 return하도록 solution 함수를 완성해주세요.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/secret.png "문제")


### 접근 방법
리스트 안에 모든 알파벳을 담고 이후 skip에 해당하는 알파벳을 리스트에서 삭제시킨다.
이 후, s의 알파벳 기준으로 알파벳 전체 집합의 최대값이 넘어 간다면 다시 a부터 시작하는 조건문을 걸어 줌.
결과는 런타임 에러가 나옴.
아무레도 반복문을 많이 쓰다보니 런타임 에러가 나온 듯 하다.


### 나의 답
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        String s = "aukks";
        String skip = "wbqd";
        int index = 5;
        String answer = "";

        List<Character> list = new ArrayList<>();

        //a~z까지 리스트 선언
        for(int i = 'a';i<='z';i++){
            list.add((char)i);
        }
        //skip에 있는 알파벳 모두 제외
        for(int i=0;i<skip.length();i++){
            list.remove(Character.valueOf(skip.charAt(i)));
        }
        System.out.println(list);

        //s에 있는 문자가 나올 경우 answer에 삽입
        for(int i=0;i<s.length();i++){
            // 이부분이 아마 런타임 에러가 뜨는 요인이 아닐까 추측
            for(int j=0;j<list.size();j++){
                //그러나 알파벳 집합의 최대값이 넘어 간다면 다시 a부터 시작하는 조건문
                if(list.size()<= j+index){
                    answer += list.get(list.size() - (j+index));
                    break;
                }
                else if(s.charAt(i) == list.get(j)){
                    answer += list.get(j+5);
                    break;
                }
            }
        }

        System.out.println(answer);

    }
}

```

### 정답 코드
```java

import java.util.*;

public class Main {

    public static void main(String[] args) {
        String s = "aukks";
        String skip = "wbqd";
        int index = 5;
        String answer = "";

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            for (int j = 0; j < index; j++) {
                c += 1;
                if (c > 'z') {
                    c -= 26;
                }
                if (skip.contains(String.valueOf(c))) {
                    j--;
                }
            }
            answer += c;
        }

        System.out.println(answer);

    }
}



```
출처: https://iyk2h.tistory.com/332


