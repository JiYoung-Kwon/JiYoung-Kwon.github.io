---
layout: post
title: '[Programmers][level2] 프린터'
subtitle: Algorithm
gh-repo: JiYoung-Kwon/JiYoung-Kwon.github.io
gh-badge: [star, fork, follow]
tags: [Algorithm, programmers]
comments: true
---

안녕하세요~ Young Blog입니다!

오랜만에 올리는 게시글은 프로그래머스 level2 프린터 문제 풀이입니다.

이 문제는 스택/큐로 분류되어 있어요~!

저는 JAVA를 사용해서 문제를 풀었습니다!

여러가지 문제에 대한 풀이 코드는 **깃허브** 를 통해서도 확인하실 수 있어요~!!

📌 [https://github.com/JiYoung-Kwon/Algorithm-study](https://github.com/JiYoung-Kwon/Algorithm-study)


***


# Problem

[programmers 코딩 테스트 고득점 Kit](https://programmers.co.kr/learn/challenges) - 스택/큐 level2 프린터 문제

##### 문제 설명

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 
이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
- 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
- location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

##### 입출력 예

| priorities         | location        | return         |
| ---------------    | --------------- |--------------- |
| [2, 1, 3, 2]       | 2               | 1              |
| [1, 1, 9, 1, 1, 1] | 0               | 5              |


##### 입출력 예 설명

- 예제 #1
문제에 나온 예와 같습니다.

- 예제 #2
6개의 문서(A, B, C, D, E, F)가 인쇄 대기목록에 있고 중요도가 1 1 9 1 1 1 이므로 C D E F A B 순으로 인쇄합니다.

<br/>

# Solution

java를 사용한 풀이입니다.

```java
import java.util.*;

class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 0;
        int k = 0;
        List<Integer> list = new ArrayList<>();
        
        for(int i= 0; i<priorities.length; i++){ // list 초기화
            list.add(priorities[i]);
        }
        
        while(!list.isEmpty()){ //모두 출력 시 종료
            int max = list.get(0);
            
            for(int i=0; i<list.size(); i++){
                if(list.get(0) < list.get(i)){ //나머지 중 큰거 있으면      
                    if(location == 0)
                        location = list.size()-1; //마지막으로
                    else
                        location--; //하나씩 땡기기                    
                    //list 첫 번째 값 -> 마지막으로 이동
                    int empty = list.get(0);
                    list.remove(0);
                    list.add(empty);
                    
                    max = 0;
                    break;          
                }
            }
            
            if(max !=0){ //중요도 제일 클 경우 출력
                list.remove(0);
                answer++;
                
                if(location == 0) //인쇄 요청 문서 출력 시 종료
                    break;
                else
                    location--; //땡기기
            }
        }
        return answer;
    }
}
```
