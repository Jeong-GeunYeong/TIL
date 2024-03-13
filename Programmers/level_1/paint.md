# 덧칠하기

### 문제 설명
어느 학교에 페인트가 칠해진 길이가 n미터인 벽이 있습니다. 벽에 동아리 · 학회 홍보나 회사 채용 공고 포스터 등을 게시하기 위해 테이프로 붙였다가 철거할 때 떼는 일이 많고 그 과정에서 페인트가 벗겨지곤 합니다. 페인트가 벗겨진 벽이 보기 흉해져 학교는 벽에 페인트를 덧칠하기로 했습니다.

넓은 벽 전체에 페인트를 새로 칠하는 대신, 구역을 나누어 일부만 페인트를 새로 칠 함으로써 예산을 아끼려 합니다. 이를 위해 벽을 1미터 길이의 구역 n개로 나누고, 각 구역에 왼쪽부터 순서대로 1번부터 n번까지 번호를 붙였습니다. 그리고 페인트를 다시 칠해야 할 구역들을 정했습니다.

벽에 페인트를 칠하는 롤러의 길이는 m미터이고, 롤러로 벽에 페인트를 한 번 칠하는 규칙은 다음과 같습니다.

롤러가 벽에서 벗어나면 안 됩니다.
구역의 일부분만 포함되도록 칠하면 안 됩니다.
즉, 롤러의 좌우측 끝을 구역의 경계선 혹은 벽의 좌우측 끝부분에 맞춘 후 롤러를 위아래로 움직이면서 벽을 칠합니다. 현재 페인트를 칠하는 구역들을 완전히 칠한 후 벽에서 롤러를 떼며, 이를 벽을 한 번 칠했다고 정의합니다.

한 구역에 페인트를 여러 번 칠해도 되고 다시 칠해야 할 구역이 아닌 곳에 페인트를 칠해도 되지만 다시 칠하기로 정한 구역은 적어도 한 번 페인트칠을 해야 합니다. 예산을 아끼기 위해 다시 칠할 구역을 정했듯 마찬가지로 롤러로 페인트칠을 하는 횟수를 최소화하려고 합니다.

정수 n, m과 다시 페인트를 칠하기로 정한 구역들의 번호가 담긴 정수 배열 section이 매개변수로 주어질 때 롤러로 페인트칠해야 하는 최소 횟수를 return 하는 solution 함수를 작성해 주세요.




### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/paint.png "문제")



### 접근 방법
HashMap을 사용하여 페인트를 칠해야하는 부분과 순서를 구분하였으며, 페인트를 칠 할 경우에는 반복문을 이용하여 총 몇롤을 칠했는지 구분하였음.


### 나의 답
```java

import java.util.*;

public class Main {

    public static void main(String[] args) {
        int n=8; // 페인트가 칠해진 길이 n
        int m=4; // 벽을 칠하는 롤러의 길이 m
        int[] section = {2, 3, 6}; //페인트를 칠하기로 정한 구역들의 번호가 담긴 배열

        int answer = 0; // 정답

        //int[]배열을 list로 변경
        List<Integer> list = Arrays.asList(Arrays.stream(section).boxed().toArray(Integer[]::new));

        //HashMap을 이용하여 페인트가 칠해진 벽 구분
        //false = 칠해진 벽, true = 안 칠해진 벽
        Map<Integer, Boolean> sectionMap = new HashMap<>();
        for (int i = 1; i <= n; i++) {
            if(list.contains(i)){
                sectionMap.put(i, true);
            }else{
                sectionMap.put(i, false);
            }
        }

        //안칠해진 벽을 기준으로 롤의 길이만큼 반복하여 연속 칠하기 실행
        for(int i=1; i<=sectionMap.size();i++){
            if(sectionMap.get(i).equals(true)){
                for(int j=0;j<m;j++){
                    sectionMap.put(i, false);
                    i += 1;//연속으로 칠해진 만큼  i를 더해줌
                }
                answer += 1;
                i-=1;//이거를 안해줄 경우 다음 반복문을 넘어가게 되면 결론적으로 i+=2가 되어버림.
            }
        }
        System.out.println(sectionMap);
        System.out.println(answer);
    }
}


```


