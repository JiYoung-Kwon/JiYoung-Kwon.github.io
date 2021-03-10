---
layout: post
title: '[Programmers][level2] 다리를 지나는 트럭'
subtitle: Algorithm
gh-repo: JiYoung-Kwon/JiYoung-Kwon.github.io
gh-badge: [star, fork, follow]
tags: [Algorithm, programmers]
comments: true
---

안녕하세요~ Young Blog입니다!

이번 게시글은 프로그래머스 level2 다리를 지나는 트럭 문제 풀이입니다.

이 문제는 스택/큐로 분류되어 있습니다.

저는 JAVA를 사용해서 문제를 풀었습니다!

여러가지 문제에 대한 풀이 코드는 **깃허브** 를 통해서도 확인하실 수 있어요~!!

📌 [https://github.com/JiYoung-Kwon/Algorithm-study](https://github.com/JiYoung-Kwon/Algorithm-study)


***


# Problem

[programmers 코딩 테스트 고득점 Kit](https://programmers.co.kr/learn/challenges) - 스택/큐 level2 프린터 문제

##### 문제 설명

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 
모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 
트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 
무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간	 |다리를 지난 트럭	|다리를 건너는 트럭|	대기 트럭|
| --------- | ------------   |--------------- |----------|
|0	        |[ ]             |[ ]             |[7,4,5,6] |
|1~2        |[ ]	           |[7]             |[4,5,6]   |
|3	        |[7]             |[4]	            |[5,6]     |
|4	        |[7]             |[4,5]	          |[6]       |
|5	        |[7,4]           |[5]	            |[6]       |
|6~7        |[7,4,5]         |[6]             |[ ]       |
|8	        |[7,4,5,6]       |[ ]            	|[ ]        |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 
이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

##### 제한 조건

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

##### 입출력 예

| bridge_length      | weight          | truck_weights                 |return          |
| ---------------    | --------------- |---------------                |--------------- |
| 2                  | 10              | [7,4,5,6]                     |	8             |
| 100                | 100             | [10]                          |101             |
|100                 |100              |[10,10,10,10,10,10,10,10,10,10]|110             |


[출처](http://icpckorea.org/2016/ONLINE/problem.pdf)

※ 공지 - 2020년 4월 06일 테스트케이스가 추가되었습니다.

<br/>

# Solution

java를 사용한 풀이입니다.

```java
import java.util.*;
class Solution {
    class Truck{
        public int weight;
        public int time;

        Truck(int weight, int time){
            this.weight = weight;
            this.time = time;
        }
    }

    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0; 
        int bridge_weight = 0;
        
        Queue<Truck> w_truck = new LinkedList<>(); //대기 트럭    
        Queue<Truck> b_truck = new LinkedList<>(); //다리 건너는 트럭      
        
        //대기 트럭 추가
        for(int i=0; i<truck_weights.length; i++){
            w_truck.add(new Truck(truck_weights[i],0));
        }
        
        while(!(w_truck.isEmpty() && b_truck.isEmpty())){
            answer++; 
            
            //건너는 트럭 존재할 경우
            if(!b_truck.isEmpty()){
                if((answer - b_truck.peek().time)>=bridge_length){
                    bridge_weight -= b_truck.peek().weight;
                    b_truck.poll();
                }
            }
            
            //대기트럭 존재할 경우
            if(!w_truck.isEmpty()){
                if(bridge_weight + w_truck.peek().weight <= weight){
                    bridge_weight += w_truck.peek().weight;             
                    b_truck.add(new Truck(w_truck.peek().weight,answer));
                    w_truck.poll();
                }    
            }
        }        
        return answer;
    }
}
```
