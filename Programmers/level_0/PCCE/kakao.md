# PCCE 1번 "출력"

### 문제 설명
선물을 직접 전하기 힘들 때 카카오톡 선물하기 기능을 이용해 축하 선물을 보낼 수 있습니다. 당신의 친구들이 이번 달까지 선물을 주고받은 기록을 바탕으로 다음 달에 누가 선물을 많이 받을지 예측하려고 합니다.

두 사람이 선물을 주고받은 기록이 있다면, 이번 달까지 두 사람 사이에 더 많은 선물을 준 사람이 다음 달에 선물을 하나 받습니다.
예를 들어 A가 B에게 선물을 5번 줬고, B가 A에게 선물을 3번 줬다면 다음 달엔 A가 B에게 선물을 하나 받습니다.
두 사람이 선물을 주고받은 기록이 하나도 없거나 주고받은 수가 같다면, 선물 지수가 더 큰 사람이 선물 지수가 더 작은 사람에게 선물을 하나 받습니다.
선물 지수는 이번 달까지 자신이 친구들에게 준 선물의 수에서 받은 선물의 수를 뺀 값입니다.
예를 들어 A가 친구들에게 준 선물이 3개고 받은 선물이 10개라면 A의 선물 지수는 -7입니다. B가 친구들에게 준 선물이 3개고 받은 선물이 2개라면 B의 선물 지수는 1입니다. 만약 A와 B가 선물을 주고받은 적이 없거나 정확히 같은 수로 선물을 주고받았다면, 다음 달엔 B가 A에게 선물을 하나 받습니다.
만약 두 사람의 선물 지수도 같다면 다음 달에 선물을 주고받지 않습니다.
위에서 설명한 규칙대로 다음 달에 선물을 주고받을 때, 당신은 선물을 가장 많이 받을 친구가 받을 선물의 수를 알고 싶습니다.

친구들의 이름을 담은 1차원 문자열 배열 friends 이번 달까지 친구들이 주고받은 선물 기록을 담은 1차원 문자열 배열 gifts가 매개변수로 주어집니다. 이때, 다음달에 가장 많은 선물을 받는 친구가 받을 선물의 수를 return 하도록 solution 함수를 완성해 주세요.

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
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_0/kakao.png "문제")


### 나의 답
```java
class Solution {
    public int solution(String[] friends, String[] gifts) {
        int answer = 0;
        String giver;
        //String receiver;
        int max =0;
        
        for(int i=0;i<friends.length;i++){
            giver = friends[i];
            int a =0;
            int b =0;
            for(int j=0;j<gifts.length;j++){
                if(gifts[j].contains(giver)){
                    if(giver.equals(gifts[j].substring(0, giver.length()))){
                        a += 1;
                    }
                    else{
                        b += 1;
                    }
                }
            }
            if(max <a-b){
                max = a-b;
                answer = a;
            }
            
        }
        
        return answer;
    }
}
```

### 정답 코드
```java
import java.util.*;

class Solution {
    public int solution(String[] friends, String[] gifts) {
        int answer = 0;
        // 선물을 주고 받은 기록을 이차원 배열로 기록
        int[][] giftGraph = new int[friends.length][friends.length];
        //결과 배열 :  0 받은 선물 1 준 선물 2 선물 지수 3 다음 달에 받을 선물
        int[][] result = new int[friends.length][4];
        // 친구들 이름과 index 저장
        HashMap<String , Integer > map = new HashMap<>();

        // 친구들 이름 및 인덱스 저장
        for( int i = 0 ; i < friends.length ; i++ ){
            map.put( friends[i] , i );
        }

        // giftGraph 구현
        for( String temp : gifts ){
            String[] ab = temp.split(" ");
            String A = ab[0];
            String B = ab[1];
            giftGraph[map.get(A)][map.get(B)]++;
        }

        // 각 친구들 별 result 구하기
        for( Map.Entry<String, Integer> a : map.entrySet()){
            int idx = a.getValue();
            int receivedCnt = 0;
            int givenCnt = 0;
            for( int i = 0 ; i < friends.length ; i++ ){
                givenCnt += giftGraph[idx][i];
            }
            result[idx][0] = givenCnt;

            for( int i = 0 ; i < friends.length ; i++ ){
                receivedCnt  += giftGraph[i][idx];
            }
            result[idx][1] = receivedCnt ;

            result[idx][2] = givenCnt - receivedCnt;

        }


        // 선물 그래프에서 가운데를 기준으로 위쪽만 비교
        for( int i = 0 ; i < friends.length ; i ++ ){
            // 선물 그래프에서 가운데를 기준으로 위쪽만 비교
            for ( int j = i+1 ; j < friends.length; j++ ){
                // i가 준 선물 수 와 j 가 준 선물 수가 같은 경우
                if( giftGraph[i][j] == giftGraph[j][i] ){
                    // 선물 지수가 i가 큰 경우
                    if( result[i][2] > result[j][2] ) result[i][3]++;
                    // 선물 지수가 j가 큰 경우
                    if( result[i][2] < result[j][2] ) result[j][3]++;
                    // 선물 지수가 같은 경우
                    if( result[i][2] == result[j][2] ) continue;
                }
                // i가 준 선물이 더 많을 경우
                else if ( giftGraph[i][j] > giftGraph[j][i] ) result[i][3]++;
                    // j가 준 선물이 더 많은 경우
                else if ( giftGraph[i][j] < giftGraph[j][i] ) result[j][3]++;
            }
        }

        // 결과 배열에서 최대값 구하기
        for( int i = 0; i < friends.length ; i++ ){
            if( result[i][3] > answer ) answer = result[i][3];
        }

        return answer;

    }
}
```

문제를 정확히 읽지 않아서 생기는 문제가 발생하였으며 내가 이해한 문제는 선물기대치 값이 가장 높은 인원의 값을 나타내는 것 인줄 알았지만,
문제는 선물지수가 가장 높은 값까지는 예측 했지만 동일한 선물지수일 경우를 생각하지 않은 것이 문제를 풀지 못한 이유이다.