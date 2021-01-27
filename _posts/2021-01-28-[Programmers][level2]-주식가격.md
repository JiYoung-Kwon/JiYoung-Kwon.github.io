---
layout: post
title: '[Programmers][level2] 주식가격'
subtitle: Algorithm
gh-repo: JiYoung-Kwon/JiYoung-Kwon.github.io
gh-badge: [star, fork, follow]
tags: [Algorithm, programmers]
comments: true
---

안녕하세요~ Young Blog입니다!

첫 게시글은 프로그래머스 level2 주식가격 문제 풀이입니다.

이 문제는 스택/큐로 분류되어 있어요~!

저는 JAVA를 사용해서 문제를 풀었습니다!

여러가지 문제에 대한 풀이 코드는 **깃허브** 를 통해서도 확인하실 수 있어요~!!

📌 https://github.com/JiYoung-Kwon/Algorithm-study


# Problem

[programmers 코딩 테스트 고득점 Kit](https://programmers.co.kr/learn/challenges) - 스택/큐 level2 주식가격 문제

##### 문제 설명

초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.

##### 입출력 예

| prices          | return          |
| --------------- | --------------- |
| [1, 2, 3, 2, 3] | [4, 3, 1, 1, 0] |   


##### 입출력 예 설명

- 1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.
- 2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.
- 3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.
- 4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.
- 5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.

※ 공지 - 2019년 2월 28일 지문이 리뉴얼되었습니다.

<br/>

# Solution

java를 사용한 풀이입니다.

```java
class Solution {
    public int[] solution(int[] prices) {
        int time =0;
        int pl = prices.length;
        int[] answer = new int[pl];
        for(int i =0; i<pl; i++){
            for(int j=i+1; j<pl; j++){
                if(prices[i] <= prices[j]) //가격이 떨어지지 않으면
                    time++;
                else { //가격이 떨어지면
                    time++;
                    break;
                }
            } 
            answer[i]=time; 
            time =0;
        }
        return answer;
    }
}
```
