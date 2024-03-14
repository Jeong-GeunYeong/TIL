# 카드 뭉치

### 문제 설명
코니는 영어 단어가 적힌 카드 뭉치 두 개를 선물로 받았습니다. 코니는 다음과 같은 규칙으로 카드에 적힌 단어들을 사용해 원하는 순서의 단어 배열을 만들 수 있는지 알고 싶습니다.

원하는 카드 뭉치에서 카드를 순서대로 한 장씩 사용합니다.
한 번 사용한 카드는 다시 사용할 수 없습니다.
카드를 사용하지 않고 다음 카드로 넘어갈 수 없습니다.
기존에 주어진 카드 뭉치의 단어 순서는 바꿀 수 없습니다.
예를 들어 첫 번째 카드 뭉치에 순서대로 ["i", "drink", "water"], 두 번째 카드 뭉치에 순서대로 ["want", "to"]가 적혀있을 때 ["i", "want", "to", "drink", "water"] 순서의 단어 배열을 만들려고 한다면 첫 번째 카드 뭉치에서 "i"를 사용한 후 두 번째 카드 뭉치에서 "want"와 "to"를 사용하고 첫 번째 카드뭉치에 "drink"와 "water"를 차례대로 사용하면 원하는 순서의 단어 배열을 만들 수 있습니다.

문자열로 이루어진 배열 cards1, cards2와 원하는 단어 배열 goal이 매개변수로 주어질 때, cards1과 cards2에 적힌 단어들로 goal를 만들 있다면 "Yes"를, 만들 수 없다면 "No"를 return하는 solution 함수를 완성해주세요.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/card.png "문제")



### 접근 방법
카드 뭉치는 1, 2로 고정적으로 2개의 배열 존재.
두개의 카드 뭉치를 이용하여 조합해야할 뭉치 1개의 배열 존재.
카드 뭉치 1, 2, 목표 뭉치1개 -> 총 3개의 배열 존재.
3개를 모두 리스트로 변환.
(리스트로 변환시기킨 이유는 카드 뭉치에서 사용되는 단어는 그때 그때 제거해 주기 위해서 이다.
제거 이후 다음 사용할 카드는 무조건 첫번째 카드 이기 때문에 첫자리만 그때 그때 삭제해주는 것이 용이해서 리스트를 사용.)
리스트 변환 후 반복문과 조건문을 이용하여 목표 카드 뭉치를 통해 사용할 단어 파악.
파악 후, 사용 된 단어는 카드 뭉치와 목표 뭉치에서 모두 제거.
이 후, 목표 뭉치가 빈 리스트일 경우 단어 조합이 제대로 된 경우임.
아닐 경우 카드 뭉치로 목표 뭉치 문장을 만들 수 없는 상태 임.


### 나의 답
```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        String[] cards1 = {"i", "water", "drink"};
        String[] cards2 = { "want", "to"};
        String[] goal ={"i", "want", "to", "drink", "water"};

        String answer="";

        //요소를 지울 때 리스트가 편하여 모든 배열을 리스트로 변형
        List<String> cardList1 = new ArrayList<String>(Arrays.asList(cards1));
        List<String> cardList2 = new ArrayList<String>(Arrays.asList(cards2));
        List<String> goalList = new ArrayList<String>(Arrays.asList(goal));

        //카드 뭉치에서 단어가 사용됐다면 goal에서도 단어가 사용 되었다는 뜻이므로 사용된 단어는 모두 remove 해버림.
        //goal이 빈 칸이 될 때까지 카드 조합을 진행
        while(!goalList.isEmpty()){
            //카드 뭉치 1
            //index error를 피하기 위해!cardList1.isEmpty()를 조건문에 추가
            if((!cardList1.isEmpty()) && goalList.get(0).equals(cardList1.get(0))){
                cardList1.remove(0);
                goalList.remove(0);
            }
            // 카드 뭉치 2
            //index error를 피하기 위해!cardList2.isEmpty()를 조건문에 추가
            else if((!cardList2.isEmpty()) && goalList.get(0).equals(cardList2.get(0))){
                cardList2.remove(0);
                goalList.remove(0);
            }
            // 이 외의 경우 카드 조합이 잘 이루어 지지 않은 경우와 goalList에 남은 카드가 존재 하므로 이므로 반복문 탈출
            else{
                break;
            }
        }
        //goalList에서 카드의 존재 여부
        if(goalList.isEmpty()){
            System.out.println("yes");
        }else{
            System.out.println("no");
        }
    }
}

```


