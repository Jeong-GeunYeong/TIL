# 달리기 경주

### 문제 설명
얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 players와 해설진이 부른 이름을 담은 문자열 배열 callings가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

### 문제 코드
```java
class Solution {
    public int solution(int[] bandage, int health, int[][] attacks) {
        int answer = 0;
        
        return answer;
    }
}
```

### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/running.png "문제")



### 접근 방법
버블 정렬 느낌으로 접근하였음.
----
HashMap을 이용하여 Key에 선수 이름 value에 등수를 넣어서 순위를 만들고 
HashMap으로 갱신을 시도하였음.


### 나의 답
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        String[] answer ={};
        String[] players = {"mumu", "soe", "poe", "kai", "mine"};
        String[] callings = {"kai", "kai", "mine", "mine"};

        List<String> ansArr = Arrays.asList(players);

        for(int i=0; i<callings.length; i++) {
            // 이름 불린 선수의 원래 등수
            int rank = ansArr.indexOf(callings[i]);
            // 순위가 바뀔 선수의 이름
            String name = players[rank-1];
            // 선수 등수 변경
            players[rank-1] = players[rank];
            players[rank] = name;
        }


        System.out.println(Arrays.toString(players));




    }
}
```

### 바꾼 코드
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        String[] answer ={};
        String[] players = {"mumu", "soe", "poe", "kai", "mine"};
        String[] callings = {"kai", "kai", "mine", "mine"};

        Map<String, Integer> race = new HashMap<>();
        for(int i=0; i<players.length; i++) {
            race.put(players[i], i);
        }

        // 연산 시작
        for(String player : callings) {
            // 등수 호출
            int rank = race.get(player);
            // 앞서 가던 선수 호출
            String beforePlayer = players[rank-1];

            // players 배열 갱신
            players[rank-1] = player;
            players[rank] = beforePlayer;

            // rankMap 갱신
            race.put(player, rank-1);
            race.put(beforePlayer, rank);
        }

        System.out.println(Arrays.toString(players));




    }
}
```


시간 초과가 떠서 더욱 효율적으로 짜야할 필요
