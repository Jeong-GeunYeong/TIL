# 추억 점수

### 문제 설명
사진들을 보며 추억에 젖어 있던 루는 사진별로 추억 점수를 매길려고 합니다. 사진 속에 나오는 인물의 그리움 점수를 모두 합산한 값이 해당 사진의 추억 점수가 됩니다. 예를 들어 사진 속 인물의 이름이 ["may", "kein", "kain"]이고 각 인물의 그리움 점수가 [5점, 10점, 1점]일 때 해당 사진의 추억 점수는 16(5 + 10 + 1)점이 됩니다. 다른 사진 속 인물의 이름이 ["kali", "mari", "don", "tony"]이고 ["kali", "mari", "don"]의 그리움 점수가 각각 [11점, 1점, 55점]이고, "tony"는 그리움 점수가 없을 때, 이 사진의 추억 점수는 3명의 그리움 점수를 합한 67(11 + 1 + 55)점입니다.

그리워하는 사람의 이름을 담은 문자열 배열 name, 각 사람별 그리움 점수를 담은 정수 배열 yearning, 각 사진에 찍힌 인물의 이름을 담은 이차원 문자열 배열 photo가 매개변수로 주어질 때, 사진들의 추억 점수를 photo에 주어진 순서대로 배열에 담아 return하는 solution 함수를 완성해주세요.




### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/memoryScore.png "문제")



### 접근 방법
2차원 배열을 이용하였으며, 결과는 각각 사진마다의 점수로 나옴.
총 사진이 3장일 경우 3개의 점수가 나와야 함.
이후 사진 안에 주어진 사람이 나올 때 마다 점수를 합산 해줌.



### 나의 답
```java
import java.util.*;

class Solution {
    public int[] solution(String[] name, int[] yearning, String[][] photo) {
        int[] answer = new int[photo.length];
        
        for(int i=0; i<photo.length; i++) { // 총 사진의 수
        	for(int j=0; j<photo[i].length; j++) { // 사진안의 사람의 수
        		for(int k=0; k<name.length; k++) { //계산해야할 사람의 수
        			if(photo[i][j].equals(name[k])) // 사진안의 사람과 주어진 사람이 일치할 경우에 사진에 점수를 올려줌.
                        answer[i] += yearning[k];
        		}
        	}
        }
        return answer;
    }
}
```


