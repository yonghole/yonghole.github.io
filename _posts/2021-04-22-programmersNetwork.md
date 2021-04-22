---
title: "[BFS] 프로그래머스 네트워크"
date: 2021-04-22 22:50:02
categories: Algorithm
---
# 프로그래머스 네트워크

문제 출처 : 

[https://programmers.co.kr/learn/courses/30/lessons/43162#](https://programmers.co.kr/learn/courses/30/lessons/43162#)

![_2021-04-22__10 44 08](https://user-images.githubusercontent.com/55180768/115725838-2764dc80-a3bd-11eb-8796-df4a9c9cdc6b.png)

![_2021-04-22__10 44 21](https://user-images.githubusercontent.com/55180768/115725848-29c73680-a3bd-11eb-8496-9e1a0ce6a24c.png)

![_2021-04-22__10 44 32](https://user-images.githubusercontent.com/55180768/115725853-29c73680-a3bd-11eb-9bab-212ae5a69b6c.png)

BFS를 이용하는 대표적인 유형 중 하나이다. 

노드 간의 연결 관계를 벡터를 이용한 인접 리스트로 표현한 것으로, Grouping을 하는 문제이다. 

BFS는 너비우선탐색으로, 자신이 연결된 동일 선상에 있는 노드들을 모두 골라낼 수 있다. 

따라서 BFS를 이용해 자신과 연결된 모든 노드에 방문 표시를 하고, 아직 방문하지 않은 노드 중 하나를 골라 또 다시 연결된 모든 노드에 방문 표시를 하면 결국 몇 개의 집단이 존재하는지 알 수 있게 된다 .

```cpp
#include <string>
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

bool isVisited[205];

int solution(int n, vector<vector<int>> computers) {
    int answer = 0;
    for(int i=0;i<n;i++){
    	if(!isVisited[i]){
            answer++;
            queue<int> q;
            q.push(i);
            isVisited[i] = true;
            while(!q.empty()){
                int cur = q.front();
                q.pop();
                for(int j = 0;j<n;j++){
                    if(!isVisited[j] && computers[cur][j] == 1){
                        isVisited[j] = true;
                        q.push(j);
                    }
                }
            }
        }
    }
    return answer;
}
```
