# PCCP 1번 붕대감기

### 문제 설명
어떤 게임에는 붕대 감기라는 기술이 있습니다.

붕대 감기는 t초 동안 붕대를 감으면서 1초마다 x만큼의 체력을 회복합니다. t초 연속으로 붕대를 감는 데 성공한다면 y만큼의 체력을 추가로 회복합니다. 게임 캐릭터에는 최대 체력이 존재해 현재 체력이 최대 체력보다 커지는 것은 불가능합니다.

기술을 쓰는 도중 몬스터에게 공격을 당하면 기술이 취소되고, 공격을 당하는 순간에는 체력을 회복할 수 없습니다. 몬스터에게 공격당해 기술이 취소당하거나 기술이 끝나면 그 즉시 붕대 감기를 다시 사용하며, 연속 성공 시간이 0으로 초기화됩니다.

몬스터의 공격을 받으면 정해진 피해량만큼 현재 체력이 줄어듭니다. 이때, 현재 체력이 0 이하가 되면 캐릭터가 죽으며 더 이상 체력을 회복할 수 없습니다.

당신은 붕대감기 기술의 정보, 캐릭터가 가진 최대 체력과 몬스터의 공격 패턴이 주어질 때 캐릭터가 끝까지 생존할 수 있는지 궁금합니다.

붕대 감기 기술의 시전 시간, 1초당 회복량, 추가 회복량을 담은 1차원 정수 배열 bandage와 최대 체력을 의미하는 정수 health, 몬스터의 공격 시간과 피해량을 담은 2차원 정수 배열 attacks가 매개변수로 주어집니다. 모든 공격이 끝난 직후 남은 체력을 return 하도록 solution 함수를 완성해 주세요. 만약 몬스터의 공격을 받고 캐릭터의 체력이 0 이하가 되어 죽는다면 -1을 return 해주세요.

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
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/pccp1-1.png "문제")

![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/pccp1-2.png "문제")


### 나의 답
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        int answer = 0;
        int[] bandage = {3,2,7};
        int health = 20;
        int[][] attack = {{1,15}, {5,16}, {8,6}};

        int present = health;
        boolean monster = false;
        int count=0;

        for(int i=0;i<=attack[attack.length-1][0];i++){
            monster =false;
//            System.out.println(i +"턴 시작 체력 : " + present);
            if(present <= 0){
//                System.out.println("체력이 0되어서 반복문 탈출");
                break;
            }
            else{
                //몬스터 공격
                for(int j =0;j< attack.length;j++){
                    if(i==attack[j][0]){
                        System.out.println("i 값 :" + i + ", j 값 : " + j);
                        present = present - attack[j][1];
                        count =0;
                        monster = true;
                        System.out.println("공격당한 후 체력 : " + present);
                        break;
                    }
                }
                if(monster){
                    continue;
                }

                if(present<health){
                    if(count==bandage[0]-1){
                        present += bandage[1]+bandage[2];
                        count =0;
                        System.out.println("체력 연속회복 달성 : " + present);

                    }
                    else{
                        present += bandage[1];
                        count += 1;
                        System.out.println("체력 기본회복 : " + present);

                    }
                }
            }
            System.out.println(i + " 턴이 모두 끝난 후 현제 체력 : "+ present);
            System.out.println("============================================");
        }
        if(present <=0){
            answer = -1;
        }
        else{
            answer = present;
        }






        System.out.println(answer);




    }
}
```

### 정답 코드
```java
class Solution {
    public int solution(int[] bandage, int health, int[][] attacks) {
        
        int life = health;
        int attackIdx = 0;
        int heal = 0;
        
        for (int i = 1; i <= attacks[attacks.length-1][0]; i++){
            if (i != attacks[attackIdx][0]){
                life += bandage[1];
                heal++;
                if (heal == bandage[0]){
                    life += bandage[2];
                    heal = 0;
                }
                if (life > health) life = health;
            } else {
                heal = 0;
                life -= attacks[attackIdx][1];
                attackIdx++;
                if (life <= 0) return -1;
            }
        }
        return life;
    }
}
```
출처: https://velog.io/@zinna_1109/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-PCCP-%EA%B8%B0%EC%B6%9C%EB%AC%B8%EC%A0%9C-1%EB%B2%88

문제이해를 정확히 했고 테스트 코드는 모두 맞췄음에도 불구하고 체점에서 틀려버림
뭐가 문제인지 생각해 보았을때 조건문 및 반복문을 많이 써서 그런 것 같은 느낌이다.
