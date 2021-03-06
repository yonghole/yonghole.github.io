---
title: "[BFS]프로그래머스 조이스틱"
date: 2021-04-27 03:29:31
categories: Algorithm
---
# 프로그래머스 조이스틱

문제 출처 : [https://programmers.co.kr/learn/courses/30/lessons/42860#](https://programmers.co.kr/learn/courses/30/lessons/42860#)

![_2021-04-27__3 17 22](https://user-images.githubusercontent.com/55180768/116132507-9c5f4b80-a708-11eb-9c2a-7d9812723694.png)


그리디 알고리즘에 속해있는 문제였지만 그리디로는 어떻게 풀어야할지 잘 떠오르지 않아 BFS를 이용하였다. 

BFS는 최단 거리를 보장하기 때문이다. 

BFS queue에 들어갈 자료형은 tuple을 이용했다. 

```cpp
// 현재 문자열, 커서의 위치, 조작횟수
queue<tuple<string,int,int> > q;
q.push(make_tuple(init,0,0)); // init은 "AAA..."와 같은 문자열이다.
```

처음에는 문자열의 맨 처음 자리에서 시작하게 된다. 

만약 현재 문자열("AAA...")의 커서 위치의 문자가 정답 문자열과 다르다면 조이스틱을 아래 위로 조작하여 문자를 같게 맞춰줘야 한다. 

```cpp
if(cur_string[cur_idx] != name[cur_idx]){
     int dif_neg = 'A' - name[cur_idx] + 26;
     int dif_pos = name[cur_idx]-'A';
     int tmp = abs(dif_neg) > abs(dif_pos) ? abs(dif_pos) : abs(dif_neg);
     cur_sum += tmp;
     cur_string[cur_idx] = name[cur_idx];
        }
```

문자가 다른 경우에 위로 조작하는 경우와 아래로 조작하는 경우가 모두 존재하는데, 두 경우를 모두 계산하고 둘 중 더 작은 것을 택한다. 

그리고 조작한만큼 cur_sum에 더해준다.

만약 현재 커서가 위치한 곳의 문자를 같게 맞춰주었는데 두 문자열이 같아진 경우, 최소 조작 횟수를 찾아낸 것으로 간주하고 cur_sum을 반환한다. 

만약 그렇지 않다면, 조이스틱을 왼쪽 또는 오른쪽으로 조작하여 다음 문자를 바꿔줘야 한다. 

따라서 조이스틱을 오른쪽으로 조작하는 경우와 왼쪽으로 조작하는 경우로 나눠 queue에 넣어준다. 

```cpp
if(cur_string == name){
            cout << cur_string;
            return cur_sum;
        }
        else{
            int pos_idx = cur_idx + 1;
            if(pos_idx >= name.size()) pos_idx = 0;
            int neg_idx = cur_idx - 1;
            if(neg_idx < 0) neg_idx = name.size()-1;
            q.push(make_tuple(cur_string,pos_idx,cur_sum+1));
            q.push(make_tuple(cur_string,neg_idx,cur_sum+1));
        }
```

만약 문제에 메모리 혹은 시간 제한이 있었다면 위와 같은 방법을 사용하면 안된다. 

왜냐하면, 조이스틱을 왼쪽 혹은 오른쪽으로 조작하는 과정에서, 직전에 있던 곳까지 (이미 같다고 확인된 곳) 모두 queue에 넣어주기 때문에 비효율적이기 때문이다. 

따라서 메모리 혹은 시간 제한이 있다면, 구조체를 활용해 네 개의 변수를 이용하는 방법도 생각해볼 수 있다. 

다만 그리디 알고리즘 문제이기 때문에 그리디 알고리즘으로 푸는 방법도 다시 생각해봐야겠다. 

```cpp
#include <string>
#include <vector>
#include <iostream>
#include "math.h"
#include <queue>
#include <tuple>
using namespace std;

int solution(string name) {
    int answer = 0;
    string init="";
    for(int i=0;i<name.size();i++){
       init.append("A"); 
    }
    
    queue<tuple<string,int,int> > q;
    q.push(make_tuple(init,0,0));
    
   	while(!q.empty()){
        tuple<string,int,int> cur = q.front();
       	q.pop();
        
        
       	
        string cur_string = get<0>(cur);
        int cur_idx = get<1>(cur);
        int cur_sum = get<2>(cur);
        
        if(cur_string[cur_idx] != name[cur_idx]){
        	int dif_neg = 'A' - name[cur_idx] + 26;
       		int dif_pos = name[cur_idx]-'A';
    		int tmp = abs(dif_neg) > abs(dif_pos) ? abs(dif_pos) : abs(dif_neg);
            cur_sum += tmp;
            cur_string[cur_idx] = name[cur_idx];
        }
        if(cur_string == name){
            cout << cur_string;
            return cur_sum;
        }
        else{
            int pos_idx = cur_idx + 1;
            if(pos_idx >= name.size()) pos_idx = 0;
            int neg_idx = cur_idx - 1;
            if(neg_idx < 0) neg_idx = name.size()-1;
            q.push(make_tuple(cur_string,pos_idx,cur_sum+1));
            q.push(make_tuple(cur_string,neg_idx,cur_sum+1));
        }
        
    } 
    
    return answer;
}
```
