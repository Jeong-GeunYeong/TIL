# PCCE 1번 "출력"

### 문제 설명
AI 엔지니어인 현식이는 데이터를 분석하는 작업을 진행하고 있습니다. 데이터는 ["코드 번호(code)", "제조일(date)", "최대 수량(maximum)", "현재 수량(remain)"]으로 구성되어 있으며 현식이는 이 데이터들 중 조건을 만족하는 데이터만 뽑아서 정렬하려 합니다.

예를 들어 다음과 같이 데이터가 주어진다면

data = [[1, 20300104, 100, 80], [2, 20300804, 847, 37], [3, 20300401, 10, 8]]
이 데이터는 다음 표처럼 나타낼 수 있습니다.

code|	date|	maximum	remain  
1	|20300104|	100|	80  
2	|20300804	|847	|37  
3	|20300401	|10	|8  
주어진 데이터 중 "제조일이 20300501 이전인 물건들을 현재 수량이 적은 순서"로 정렬해야 한다면 조건에 맞게 가공된 데이터는 다음과 같습니다.

data = [[3,20300401,10,8],[1,20300104,100,80]]
정렬한 데이터들이 담긴 이차원 정수 리스트 data와 어떤 정보를 기준으로 데이터를 뽑아낼지를 의미하는 문자열 ext, 뽑아낼 정보의 기준값을 나타내는 정수 val_ext, 정보를 정렬할 기준이 되는 문자열 sort_by가 주어집니다.

data에서 ext 값이 val_ext보다 작은 데이터만 뽑은 후, sort_by에 해당하는 값을 기준으로 오름차순으로 정렬하여 return 하도록 solution 함수를 완성해 주세요. 단, 조건을 만족하는 데이터는 항상 한 개 이상 존재합니다.

### 문제
```java
class Solution {
    public int[][] solution(int[][] data, String ext, int val_ext, String sort_by) {
        int[][] answer = {};
        return answer;
    }
}
```

### 출력 예시
![문제](https://raw.githubusercontent.com/Jeong-GeunYeong/TIL/master/image/codingTest/Programmers/level_0/pcce10.png "문제")


### 나의 답
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Main {

    public static void main(String[] args) {
        int answer = 0;

        int data[][] = {{1, 20300104, 100, 80}, {2, 20300804, 847, 37}, {3, 20300401, 10, 8}};
        String ext = "data";
        int val_ext = 20300501;
        String sort_by ="remain";

        //code, date, maximum, remain
//        int[] test = new int[4];
        Map <Integer, int[]> map = new HashMap<Integer, int[]>();

        if(ext.equals("data")){
            for(int i=0;i< data.length;i++){
                int[] test = new int[4];
                if(data[i][1]<val_ext){
                    for(int j=0;j<data[i].length;j++){
                        System.out.println(data[i][j]);
                        test[j] = data[i][j];
                    }
                    map.put(data[i][1], test);
                }
            }
        }
        System.out.println("::"+map);
        



        System.out.println(answer);




    }
}
```

### 정답 코드
```java
import java.util.*;
class Solution {
    int sort_by_Num = 0; // sortBy 인덱스 구하기
    public int[][] solution(int[][] data, String ext, int val_ext, String sort_by) {
        
        String[] dataArr = {"code","date","maximum","remain"};
        int extNum = 0; // ext의 인덱스 구하기
        
        for(int i =0; i<dataArr.length; i++) {
            if(dataArr[i].equals(ext)) {
                extNum = i;
            }
            if(dataArr[i].equals(sort_by)) {
                sort_by_Num = i;
            }
        }
        
        List<Integer[]> dataList = new ArrayList<>();
        for(int i =0; i<data.length; i++) {
            if(data[i][extNum] < val_ext) {
                dataList.add(Arrays.stream(data[i]).boxed().toArray(Integer[]::new));
            }
        }
        
        Collections.sort(dataList, new Comparator<Integer[]>() {
            @Override
            public int compare(Integer[] arr1, Integer[] arr2) {
                // 특정 인덱스의 값으로 비교하여 정렬
                return Integer.compare(arr1[sort_by_Num], arr2[sort_by_Num]);
            }
        });

        int[][] answer = new int[dataList.size()][dataList.get(0).length];
        for (int i = 0; i < dataList.size(); i++) {
            answer[i] = Arrays.stream(dataList.get(i))
                               .mapToInt(Integer::intValue)
                               .toArray();
        }
        
        return answer;
    }
    

}
```

정렬을 해야하는 문제인 것을 파악은 했으며 컬렉션을 이용할 경우 매 간단하게 접근이 가능 그러나 배열의 값을 추출하는 것 에서 막힘이 있었으며 값을 문자열에서 정수형, 정수형에서 다시 문자열러 바꾸는데 뇌사가 옴


