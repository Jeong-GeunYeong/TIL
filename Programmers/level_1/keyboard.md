# 대충 만든 자판

### 문제 설명
휴대폰의 자판은 컴퓨터 키보드 자판과는 다르게 하나의 키에 여러 개의 문자가 할당될 수 있습니다. 키 하나에 여러 문자가 할당된 경우, 동일한 키를 연속해서 빠르게 누르면 할당된 순서대로 문자가 바뀝니다.

예를 들어, 1번 키에 "A", "B", "C" 순서대로 문자가 할당되어 있다면 1번 키를 한 번 누르면 "A", 두 번 누르면 "B", 세 번 누르면 "C"가 되는 식입니다.

같은 규칙을 적용해 아무렇게나 만든 휴대폰 자판이 있습니다. 이 휴대폰 자판은 키의 개수가 1개부터 최대 100개까지 있을 수 있으며, 특정 키를 눌렀을 때 입력되는 문자들도 무작위로 배열되어 있습니다. 또, 같은 문자가 자판 전체에 여러 번 할당된 경우도 있고, 키 하나에 같은 문자가 여러 번 할당된 경우도 있습니다. 심지어 아예 할당되지 않은 경우도 있습니다. 따라서 몇몇 문자열은 작성할 수 없을 수도 있습니다.

이 휴대폰 자판을 이용해 특정 문자열을 작성할 때, 키를 최소 몇 번 눌러야 그 문자열을 작성할 수 있는지 알아보고자 합니다.

1번 키부터 차례대로 할당된 문자들이 순서대로 담긴 문자열배열 keymap과 입력하려는 문자열들이 담긴 문자열 배열 targets가 주어질 때, 각 문자열을 작성하기 위해 키를 최소 몇 번씩 눌러야 하는지 순서대로 배열에 담아 return 하는 solution 함수를 완성해 주세요.

단, 목표 문자열을 작성할 수 없을 때는 -1을 저장합니다.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/keyboard.png "문제")



### 접근 방법
자판의 개수가 많을 수도 있으므로 중복 제거가 필요하다고 생각했음.
그러고 중복의 경우 최소 값을 기준으로 가져가야해서 중복제거 기준을 최소값을 기준으로 가짐.\
HashMap을 선언하여 K: 알파벳, V: 횟수 를 저장 함.
HashMap을 이용하여 중복 값을 제거 하고 조건문을 이용하여 최소값 기준을 나눔.
이 후, 만들어진 HashMap을 이용하여 targets에 담긴 문자의 요소 마다 count를 더하여 결과 값 출력.
해당되는 단어가 없는 경우 count에 -1를 넣어 줌.

### 나의 답
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        String[] keymap ={"ABACD", "BCEFD"};
        String[] targets = {"ABCD","AABB"};

        int[] answer = new int[targets.length]; // 정답

        HashMap<Character, Integer> map = new HashMap<>();

        for(int i=0;i<keymap.length;i++){
            for(int j=0;j<keymap[i].length();j++){
                if(map.containsKey(keymap[i].charAt(j))){
                    //cnt를 사용안하고 map.get을 할 경우 런타임 에러가 생김.
                    Integer cnt = map.get(keymap[i].charAt(j));
                    if(cnt>(j+1)){
                        map.put(keymap[i].charAt(j),j+1);
                    }
                }else{
                    map.put(keymap[i].charAt(j), j+1);
                }
            }
        }

        for(int i=0;i<targets.length;i++){
            int count=0;
            for(int j=0;j<targets[i].length();j++){

                //이부분이 내가 만든 초기 코드
                if(map.containsKey(targets[i].charAt(j))){
                    count += map.get(targets[i].charAt(j));
                }
                else{
                    count = -1;
                    break;
                }

            }
            answer[i] = count;
        }
        System.out.println(Arrays.toString(answer));
    }
}
```


