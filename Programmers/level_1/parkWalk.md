# 달리기 경주

### 문제 설명
지나다니는 길을 'O', 장애물을 'X'로 나타낸 직사각형 격자 모양의 공원에서 로봇 강아지가 산책을 하려합니다. 산책은 로봇 강아지에 미리 입력된 명령에 따라 진행하며, 명령은 다음과 같은 형식으로 주어집니다.

["방향 거리", "방향 거리" … ]
예를 들어 "E 5"는 로봇 강아지가 현재 위치에서 동쪽으로 5칸 이동했다는 의미입니다. 로봇 강아지는 명령을 수행하기 전에 다음 두 가지를 먼저 확인합니다.

주어진 방향으로 이동할 때 공원을 벗어나는지 확인합니다.
주어진 방향으로 이동 중 장애물을 만나는지 확인합니다.
위 두 가지중 어느 하나라도 해당된다면, 로봇 강아지는 해당 명령을 무시하고 다음 명령을 수행합니다.
공원의 가로 길이가 W, 세로 길이가 H라고 할 때, 공원의 좌측 상단의 좌표는 (0, 0), 우측 하단의 좌표는 (H - 1, W - 1) 입니다.

공원을 나타내는 문자열 배열 park, 로봇 강아지가 수행할 명령이 담긴 문자열 배열 routes가 매개변수로 주어질 때, 로봇 강아지가 모든 명령을 수행 후 놓인 위치를 [세로 방향 좌표, 가로 방향 좌표] 순으로 배열에 담아 return 하도록 solution 함수를 완성해주세요.


### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/park.png "문제")



### 접근 방법
공원의 크기는 직사각형 형태로 고정되며, 시작 위치만 찾아낸다면 2차원 배열에서 이동은 크게 어렵지 않음.


### 나의 답
```java
class Solution {
    public int[] solution(String[] park, String[] routes) {
        
        int parkH =park.length;
        int parkW =park[0].length();
        int robotH =0;
        int robotW =0;
        
        String[][] parkCo = new String[parkH][parkW];
        for(int i=0; i<parkH;i++){
            String[] parkap = park[i].split("");
            for(int j=0; j<parkW;j++){
                parkCo[i][j]=parkap[j];
            }
        }
        for(int i=0;i<parkH;i++){
            for(int j=0;j<parkW;j++){
                if(parkCo[i][j].equals("S")){
                    robotH=i;
                    robotW=j;
                    break;
                }
            }
        }
        for(int i=0; i<routes.length;i++){
            String[] spl = routes[i].split(" ");
            int time = Integer.parseInt(spl[1]);//반복횟수는 time으로
            boolean go = true;
            switch(spl[0]){
                case "N"://H줄이기
                    if(robotH-time<0){break;}
                    for(int n=1;n<=time;n++){
                        if(parkCo[robotH-n][robotW].equals("X")){go = false;}
                    }
                    if(go==false){break;}
                    robotH-=time;
                    break;
                case "S"://H늘리기
                    if(robotH+time>=parkH){break;}
                    for(int n=1;n<=time;n++){
                        if(parkCo[robotH+n][robotW].equals("X")){go = false;}
                    }
                    if(go==false){break;}
                    robotH+=time;
                    break;
                case "W"://W줄이기
                    if(robotW-time<0){break;}
                     for(int n=1;n<=time;n++){
                        if(parkCo[robotH][robotW-n].equals("X")){go = false;}
                    }
                    if(go==false){break;}
                    robotW-=time;
                    break;
                case "E"://W늘리기
                    if(robotW+time>=parkW){break;}
                    for(int n=1;n<=time;n++){
                        if(parkCo[robotH][robotW+n].equals("X")){go = false;}
                    }
                    if(go==false){break;}
                    robotW+=time;
                    break;
            }
        }
        int[] answer = new int[2];
        answer[0] = robotH;
        answer[1] = robotW;        
        return answer;
    }
}

```

