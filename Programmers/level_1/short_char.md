# 크기가 작은 부분 문자열

### 문제 설명
숫자로 이루어진 문자열 t와 p가 주어질 때, t에서 p와 길이가 같은 부분문자열 중에서, 이 부분문자열이 나타내는 수가 p가 나타내는 수보다 작거나 같은 것이 나오는 횟수를 return하는 함수 solution을 완성하세요.

예를 들어, t="3141592"이고 p="271" 인 경우, t의 길이가 3인 부분 문자열은 314, 141, 415, 159, 592입니다. 이 문자열이 나타내는 수 중 271보다 작거나 같은 수는 141, 159 2개 입니다.

### 제한 사항
- 1 ≤ p의 길이 ≤ 18
- p의 길이 ≤ t의 길이 ≤ 10,000
- t와 p는 숫자로만 이루어진 문자열이며, 0으로 시작하지 않습니다.



### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_1/short_char.png "문제")


### 접근 방법
문제 설명에 "t="3141592"이고 p="271" 인 경우, t의 길이가 3인 부분 문자열은 314, 141, 415, 159, 592입니다." 이 부분에서 한자리식 늘어나는 걸 확인했다.
내 접근 방법은 p의 길이만큼 추출하고 첫번째 자리를 삭제하면 다시 처음 3자리만 추출하면 되기에 반복문 마지막에 t의 첫자리를 삭제해주면서 진행하는 방식을 택하였음.

그리고 
int형의 최대값은 2,147,483,647 이며
p의 문자열 길이는 최대 18자리이다.
그러므로 자릿수를 초과하게 되며 이로써 int가 아닌 long을 사용해야 함.




### 나의 답
```java
public class Main {

    public static void main(String[] args) {
        //예시 코드
        String t = "3141592";
        String p = "271";

        int answer = 0;

        //반복문의 길이설정을 미리하는 이유는 t.substring을 할경우 length의 길이가 한칸씩 줄며 i의 값은 커지므로 길이가 -2씩 되는거나 마찬가지 이므로 미리 값을 설정하여 시작.
        int length=t.length()-p.length();

        for(int i=0;i<=length;i++ ){
            //p의 길이만큼 long으로 타입 변환
            long tBox = Long.parseLong(t.substring(0,p.length()));
            long pBox = Long.parseLong(p);

            //추출한 값과 비교대상값을 비교
            if(tBox <= pBox){
                answer +=1;

            }
            //추출문자에서 첫문자 삭제
            t = t.substring(1);
        }
        System.out.println("-------------------------");
        System.out.println(answer);
    }
}
```
