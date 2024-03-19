# 카드 뭉치

### 문제 설명
문자열 s가 주어졌을 때, s의 각 위치마다 자신보다 앞에 나왔으면서, 자신과 가장 가까운 곳에 있는 같은 글자가 어디 있는지 알고 싶습니다.
예를 들어, s="banana"라고 할 때,  각 글자들을 왼쪽부터 오른쪽으로 읽어 나가면서 다음과 같이 진행할 수 있습니다.

b는 처음 나왔기 때문에 자신의 앞에 같은 글자가 없습니다. 이는 -1로 표현합니다.
a는 처음 나왔기 때문에 자신의 앞에 같은 글자가 없습니다. 이는 -1로 표현합니다.
n은 처음 나왔기 때문에 자신의 앞에 같은 글자가 없습니다. 이는 -1로 표현합니다.
a는 자신보다 두 칸 앞에 a가 있습니다. 이는 2로 표현합니다.
n도 자신보다 두 칸 앞에 n이 있습니다. 이는 2로 표현합니다.
a는 자신보다 두 칸, 네 칸 앞에 a가 있습니다. 이 중 가까운 것은 두 칸 앞이고, 이는 2로 표현합니다.
따라서 최종 결과물은 [-1, -1, -1, 2, 2, 2]가 됩니다.

문자열 s이 주어질 때, 위와 같이 정의된 연산을 수행하는 함수 solution을 완성해주세요.

### 제한 사항
- 1 ≤ s의 길이 ≤ 10,000
- s은 영어 소문자로만 이루어져 있습니다.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/near_char.png "문제")



### 접근 방법
자신보다 앞에 나왔으면서, 자신과 가장 가까운 곳에 있는 글자 기준.
거꾸로 생각해 보면 reverse기준 자신보다 뒤에 나왔으면서 자신과 가장 가까운 곳에 있는 글자를 찾으면 되는 문제.
글자를 거꾸로 놓고 생각하였음.


### 나의 답
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
//        String s= "banana";
        String s = "foobar";

        //s의 길이 만큼 정답이 나와야 함.
        int[] answer = new int[s.length()];

        //자신보다 앞에 나왔으면서, 자신과 가장 가까운 곳에 있는 글자 기준
        //거꾸로 생각해 보면 reverse기준 자신보다 뒤에 나왔으면서 자신과 가장 가까운 곳에 있는 글자
        for(int i=s.length()-1;i>=0;i--){
            for(int j=s.length()-1;j >=0;j--){
                //i>j 이거를 넣어주지 않을 경우 같은 위치의 글자는 항상 같다고 나오므로 i-j가 0으로 나옴.
                if(i>j&&s.charAt(i)==s.charAt(j)){
                    answer[i] = i-j;
                    break;
                }else{
                    answer[i] = -1;
                }
            }
        }

        System.out.println(Arrays.toString(answer));
    }
}



```


