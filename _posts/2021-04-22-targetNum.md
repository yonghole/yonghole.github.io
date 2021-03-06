---
title: "[DFS]프로그래머스 타겟넘버"
date: 2021-04-22 15:40:03
categories: Algorithm
---
# 프로그래머스 타겟넘버

문제 출처 : 

[코딩테스트 연습 - 타겟 넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

![_2021-04-22__3 21 19](https://user-images.githubusercontent.com/55180768/115667792-3463da80-a381-11eb-84a4-65ac48b6e7ec.png)

DFS를 이용해 각 자리 숫자를 적절히 더하고 빼는 경우를 모두 테스트해주면 된다. 

문제를 잘못 이해해 복잡하게 생각하면

5+4+3+2+1 = 15 와

1+2+3+4+5 = 15 가 다른 경우라고 생각하게 되는데, 이렇게 하면 문제가 상당히 복잡해진다. 

만약 두 경우를 다른 경우로 가정해야 하는 문제였다면 

1+1+1+1+1 = 15도 복수 개가 있었어야 하지만 그렇지 않기 때문에, 

1. 각 자리에서 + 인 경우
2. 각 자리에서 - 인 경우

이렇게 두 가지 경우를 가정하고 두 가지 상황에 대해 모두 dfs를 확인해줘야 한다. 

dfs 함수는 몇 개의 수를 이용했는지를 나타내는 매개변수 n 과, 현재까지의 합을 나타내는 curSum 매개변수를 받는다. 

만약 n 이 전체 숫자 개수와 동일하다면 (모든 숫자를 다 더함) curSum이 target과 같은지 확인하면 된다. 

만약 그렇지 않다면, 

1. 현재 위치의 수 (numbers 배열에서 n 번째)를 + 로 두고 dfs 진행
2. 현재 위치의 수 (numbers 배열에서 n 번째)를 - 로 두고 dfs 진행

의 과정을 거치면 된다. 

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int arr[25];
bool isUsed[25];
int numSize,tgt;
int result=0;
vector<int> tmp;
void dfs(int n,int curSum){
    if(n == numSize){
        if(curSum == tgt){
            result++;
        }
        return;
    }
    		dfs(n+1,curSum+arr[n]);
    		dfs(n+1,curSum-arr[n]);  
}

int solution(vector<int> numbers, int target) {
    for(int i=0;i<numbers.size();i++){
        arr[i] = numbers[i];
    }
    numSize = numbers.size();
    tgt = target;
    int answer = 0;
    dfs(0,0);
    answer = result;
    return answer;
}
```
