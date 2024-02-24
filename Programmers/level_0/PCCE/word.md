# PCCE 1번 "출력"

### 문제 설명
문자열 my_string, overwrite_string과 정수 s가 주어집니다. 문자열 my_string의 인덱스 s부터 overwrite_string의 길이만큼을 문자열 overwrite_string으로 바꾼 문자열을 return 하는 solution 함수를 작성해 주세요.

### 문제
```java
class Solution {
    public int solution(String[] friends, String[] gifts) {
        int answer = 0;
        return answer;
    }
}
```

### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_0/word.png "문제")


### 나의 답
```java
class Solution {
    public String solution(String my_string, String overwrite_string, int s) {
        String answer = "";
        
       answer = my_string.substring(s, s+overwrite_string.length());
       my_string = my_string.replace(answer, overwrite_string);        
       answer = my_string;

       return answer;
 
    }
}
```

### 정답 코드
```java
class Solution {
    public String solution(String my_string, String overwrite_string, int s) {
        String answer = "";
        
     //   answer = my_string.substring(s, s+overwrite_string.length());
   //     my_string = my_string.replace(answer, overwrite_string);        
 //       answer = my_string;
            
        answer = my_string.substring(0,s) + overwrite_string 
            + my_string.substring(s+overwrite_string.length(),my_string.length());
        
        
        return answer;
    }
}
```

이 문제의 경우 정답은 원하는대로 나왔지만 테스트를 돌렸을 경우 6번 테스트에서 자꾸 실패했으며 아마 메모리가 허용된 것 보다 초과되는 것으로 보임.



