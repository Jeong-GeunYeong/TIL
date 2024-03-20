# 카드 뭉치

### 문제 설명
문자열 s가 입력되었을 때 다음 규칙을 따라서 이 문자열을 여러 문자열로 분해하려고 합니다.

먼저 첫 글자를 읽습니다. 이 글자를 x라고 합시다.
이제 이 문자열을 왼쪽에서 오른쪽으로 읽어나가면서, x와 x가 아닌 다른 글자들이 나온 횟수를 각각 셉니다. 처음으로 두 횟수가 같아지는 순간 멈추고, 지금까지 읽은 문자열을 분리합니다.
s에서 분리한 문자열을 빼고 남은 부분에 대해서 이 과정을 반복합니다. 남은 부분이 없다면 종료합니다.
만약 두 횟수가 다른 상태에서 더 이상 읽을 글자가 없다면, 역시 지금까지 읽은 문자열을 분리하고, 종료합니다.
문자열 s가 매개변수로 주어질 때, 위 과정과 같이 문자열들로 분해하고, 분해한 문자열의 개수를 return 하는 함수 solution을 완성하세요.

### 제한 사항
- 1 ≤ s의 길이 ≤ 10,000
- s은 영어 소문자로만 이루어져 있습니다.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/divide_char.png "문제")



### 접근 방법
x를 기준값으로 잡고 x의 크기를 count로 잡습니다.
다음 x와 같은 값이 나올경우 count를 올려준고, 다른값일 경우 count를 내려줍니다.
이후 count가 0이 되는 기점으로 x의 값을 바꿔줍니다.


### 나의 답
```java
public class Main {

    public static void main(String[] args) {
        String s= "aaabbaccccabba";

        // 1부터 시작
        int answer = 1;

        //첫째 자리는 이미 존재하니 1 부터 시작
        int count =1;
        //기준 값
        char x = s.charAt(0);

        for(int i=1;i<s.length();i++){
            //count가 0이 될 경우 서로 다른 문자의 개수가 같아지는 지점
            if(count ==0){
                answer++;
                //기준 값 다음으로 교체
                x=s.charAt(i);
            }

            //값이 같을 경우 count를 올려주고 다를경우 내려줌
            if(x == s.charAt(i)){
                count++;
            }
            else{
                count--;
            }
        }

        System.out.println(answer);
    }
}


```


