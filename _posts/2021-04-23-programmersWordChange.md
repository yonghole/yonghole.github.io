---
title: "[BFS] 프로그래머스 단어 변환"
date: 2021-04-23 01:08:18
categories: Algorithm
---
# 프로그래머스 단어 변환

문제 출처 : [문제출처-프로그래머스_단어_변환](https://programmers.co.kr/learn/courses/30/lessons/43163)

![_2021-04-22__11 44 22](https://user-images.githubusercontent.com/55180768/115747400-3012de00-a3d0-11eb-8352-10e32eb9f2b6.png)

한 개의 알파벳만 바꿀 수 있다는 조건 때문에 까다로워 보이지만 인접리스트를 이용해 단어들 사이의 관계를 미리 정리해놓으면 복잡하지 않게 해결할 수 있다. 

우선, begin을 포함한 모든 단어들의 관계를 정리해야 한다. 

string으로 관계를 정리하는 것보다는 인덱스로 배열을 관리하는 것이 낫다고 생각해, 인덱스를 이용해 단어들을 정리해주었다. 

```cpp
vector< vector<int> > v;
for(int i=0;i<words.size();i++){
        if(words[i] == target) target_idx = i;
        vector<int> tp;
        for(int j=0;j<words.size();j++){
            if(j!=i){
                int tmp = 0;
                for(int x=0;x<words[0].size();x++){
                    if(words[i][x] != words[j][x]) tmp ++;
                    if(tmp > 1) break;
                }
                if(tmp == 1){
                    tp.push_back(j);
                }
            }
        }
        v.push_back(tp);
    }
```

모든 단어는 words 배열 내의 index로 다룬다. 

words 배열 내의 모든 단어들에 대해, 알파벳 하나만 차이가 나는 단어들을 각 인덱스의 벡터로 넣는다. 

begin의 경우 words 배열 내에 없기 때문에 따로 처리해줘야한다. 

이렇게 되면 다음과 같이 정리될 수 있다. 

![IMG_2648](https://user-images.githubusercontent.com/55180768/115747418-343efb80-a3d0-11eb-9651-d349a1568e26.jpg)

이제 begin부터 시작해 자신이 선택할 수 있는 단어들(알파벳 하나만 바꿔 만들 수 있는 단어들)을 이용해 BFS를 수행하면 된다. 

BFS는 최소 거리를 보장하기 때문에, 가장 먼저 target 단어가 나오는 순간이 begin에서 target으로 갈 수 있는 최소 단계가 되는 순간이다. 

몇 단계를 거쳐서 현재 단어로 온 것인지 알기 위해 BFS를 수행할 때 이용하는 queue는 pair<int,int> 형으로 만든다. 

pair는 

first = 단어의 인덱스 값

second = 현재 단계

단계는 처음 0부터 시작해 queue에 들어가는 순간 +1 된다. 

```cpp
#include <string>
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

bool isUsed[55];

int solution(string begin, string target, vector<string> words) {
    int answer = 0;
    int begin_idx = 55;
    int target_idx = -1;
    vector< vector<int> > v;
    vector<int> for_begin;
    for(int j=0;j<words.size();j++){
        int tmp = 0;
        for(int x=0;x<words[0].size();x++){
        	if(begin[x] != words[j][x]) tmp ++;
               if(tmp > 1) break;
        }
        if(tmp == 1) for_begin.push_back(j);
                
    }
    
    for(int i=0;i<words.size();i++){
        if(words[i] == target) target_idx = i;
        vector<int> tp;
        for(int j=0;j<words.size();j++){
            if(j!=i){
                int tmp = 0;
                for(int x=0;x<words[0].size();x++){
                    if(words[i][x] != words[j][x]) tmp ++;
                    if(tmp > 1) break;
                }
                if(tmp == 1){
                    tp.push_back(j);
                }
            }
        }
        v.push_back(tp);
    }
    if(target_idx == -1) return 0;
    queue<pair<int,int> > q;
    q.push(make_pair(begin_idx,0));
    isUsed[begin_idx] = true;
    
    while(!q.empty()){
        pair<int,int> cur = q.front();
        //cout << words[cur.first];
        q.pop();
        
        if(cur.first == begin_idx){
            for(int i=0;i<for_begin.size();i++){
                isUsed[for_begin[i]] = true;
                q.push(make_pair(for_begin[i],1));
            }
        }
        else{
        	if(cur.first == target_idx){
            	cout << words[cur.first] << " " << target_idx;
            	return cur.second;
       		}
        
        	for(int i=0;i<v[cur.first].size();i++){
            	if(!isUsed[v[cur.first][i]]){
                	q.push(make_pair(v[cur.first][i],cur.second+1));
                	isUsed[v[cur.first][i]] = true;
           		}
        	}
        }
    }
    return answer;
}
```
