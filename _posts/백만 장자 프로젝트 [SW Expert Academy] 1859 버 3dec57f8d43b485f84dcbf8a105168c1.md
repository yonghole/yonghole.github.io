# 백만 장자 프로젝트 [SW Expert Academy] 1859 번

문제 : 

[SW Expert Academy](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5LrsUaDxcDFAXc&)

우선 현재에 해당하는 날에 구매를 했다면 ? 자기를 기준으로 앞으로 다가오는 날들 중에 가장 비싼 날에 팔아야 한다. 

가장 간단한 방법을 생각해보면, 자신을 기준으로 뒤에 있는 날들 중 가격이 비싼 날을 저장하고, 그 날의 가격과 자신의 날 사이의 차이를 누적하면 된다. 

그런데 앞에서부터 계산을 해간다면 뒤에 더 비싼 날이 올지 안올지 모르고, 그 경우의 수를 모두 비교해서 저장해야 한다. 

최대 날짜는 100만일이기 때문에 시간복잡도를 고려하지 않을 수 없다. 

뒤에서부터 접근한다면 이 문제는 쉽게 해결이 된다. 

맨 뒤 요소를 기준으로 앞으로 가면서 자신보다 비용이 싼 날들과의 차이를 더해주고, 더 비싼 날이 나오면 그 날을 기준으로 다시 앞으로 가면서 자신보다 비용이 싼 날들과의 차이를 더해준다. 

```cpp
#include<iostream>
 
using namespace std;
 
long long arr[1000005];
 
int main(int argc, char** argv)
{
    int test_case;
    int T;

    cin>>T;
    /*
       여러 개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
    */
    for(test_case = 1; test_case <= T; ++test_case)
    {
 
        int len;
        cin >> len;
        for(int i=0;i<len;i++){
            cin >> arr[i];
        }
        long long anc = arr[len-1];
        long long profit = 0;
        for(int i=len-1;i>=0;i--){
            if(arr[i] < anc) profit += (anc - arr[i]);
            else if(arr[i] > anc) anc = arr[i];
        }
        cout << "#" << test_case << " " << profit << "\n";
    }
     
    return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```