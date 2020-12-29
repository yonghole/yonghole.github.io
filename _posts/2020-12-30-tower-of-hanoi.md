---
title: "하노이 타워 (재귀)"
date: 2020-12-30 12:52:41
categories: Algorithm
comment : true
---



# 하노이탑

하노이탑은 가장 유명한 재귀 알고리즘 중 하나이다. 

처음 하노이탑을 접했을 때 재귀 알고리즘이 익숙치 않아 한참을 씨름했던 기억이 난다. 

재귀 알고리즘을 풀 때 가장 중요한 것은 

1. 기저 조건이 무엇인가?
2. 자신보다 작은 case를 호출할 수 있는 구조인가? 

---

### 하노이의 탑 (Tower of Hanoi)

세 개의 장대가 있고, 첫 번째 장대에는 크기가 다른 n 개의 원판이 쌓여 있다. 각 원판은 아래부터 크기가 큰 것부터 작은 것 순으로 쌓여있다. 이 때, 다음 규칙에 따라 첫 번째 장대에서 세 번째 장대로 원판들을 옮기려고 한다. 

1. 한 번에 한 개의 원탑을 다른 탑으로 옮길 수 있다. 
2. 원판은 자신보다 크기가 작은 원판의 위에 놓일 수 없다. 

이 때 원판을 옮기는데 필요한 최소 이동 횟수와 순서를 구하시오.

우선 예시를 통해 하노이탑의 과정을 살펴보자. 

다음은 원판이 3 개 있을 때의 하노이탑 과정이다. 

![hanoi1](https://user-images.githubusercontent.com/55180768/103296479-859a3800-4a39-11eb-8462-200fa11abf66.png)

초기 상태에 1번 장대에 세 개의 원판이 있다. 편의상 가장 작은 원판부터 1번 2번 3번으로 부르겠다. 우선 세 개의 원판을 모두 3번 장대로 옮기기 위해서는 가장 큰 3번 원판이 3번 장대로 이동해야 한다. 따라서 나머지 두 원판이 3번에 있지 않은 상태를 만들어야 하는데, 이 경우는 2번 장대에 1번과 2번 원판이 존재해야 한다. 차근차근 원판을 옮겨보자.

- 1번 원판을 3번 장대로 옮긴다.
![hanoi2](https://user-images.githubusercontent.com/55180768/103296484-8763fb80-4a39-11eb-9717-b605d95b591a.png)

- 2번 원판을 2번 장대로 옮긴다.

![hanoi3](https://user-images.githubusercontent.com/55180768/103296487-87fc9200-4a39-11eb-9f9b-a175e4c33365.png)

- 1번 원판을 2번 장대로 이동한다.

이제 3번 원판은 3번 장대로 이동할 수 있다.

![hanoi4](https://user-images.githubusercontent.com/55180768/103296488-88952880-4a39-11eb-9cba-d1221d174d83.png)

- 3**번 원판을 3번 장대로 이동한다.**

    이제 남은 일은, 2번 장대에 있는 원판 두 개를 3번 장대로 옮기는 것이다. 

![hanoi5](https://user-images.githubusercontent.com/55180768/103296491-892dbf00-4a39-11eb-8b55-dab9c56324d1.png)

 

- 1번 원판을 1번 장대로 옮긴다.
![hanoi6](https://user-images.githubusercontent.com/55180768/103296492-89c65580-4a39-11eb-8c5b-cabdfc0966c6.png)

- 2번 원판을 3번 장대로 옮긴다.

![hanoi7](https://user-images.githubusercontent.com/55180768/103296494-89c65580-4a39-11eb-93e9-784bc4141753.png)

- 1번 원판을 3번 장대로 옮긴다. (#7번)

![hanoi8](https://user-images.githubusercontent.com/55180768/103296495-8a5eec00-4a39-11eb-9e96-a8b34a9837b3.png)


원판이 세 개인 경우에 필요한 최소 이동 횟수는 7번이다. 

이제 문제를 해결하기 위한 조건을 찾아보자. 

### 기저 조건(base case) 찾기

---

재귀 문제에서 중요한 것은 기저 조건(base case)를 찾는 것이다. 기저 조건이 없거나 잘못되면 무한히 호출되어 끝나지 않기 때문이다. 기저 조건은 자기보다 작은 case를 호출하지 않는 경우를 얘기하며, 하노이의 탑에서 기저 조건은 간단히 찾아질 수 있다. 

***원판이 하나만 있을 때는 필요한 이동 횟수가 1회이기 때문에 기저 조건이 된다.*** 

따라서 재귀 호출이 이어져 계속 내려가다 원판이 하나인 경우가 되면, 반환점이 되는 것이다. 

### 자신보다 작은 case를 호출할 수 있는가?

---

자신보다 작은 case를 호출할 수 있는지를 알아보기 위해서는 문제를 쪼개서 볼 수 있어야 한다. 

위에서 살펴본 예시는 3 개의 원판을 1번 장대에서 3번 장대로 옮기는 문제였다. 

우리가 원하는 함수의 형태로 문제를 나타내면 다음과 같다. 

```cpp
hanoi(int plates,int src, int dst);

hanoi(3,1,3);
```

그런데, 이 문제를 해결하기 위해서 우리는 1번 원판과 2번 원판 두 개의 원판을 1번 장대에서 2번 장대로 옮겨야 했다. 이 문제도 함수로 나타내면 다음과 같다. 

```cpp
hanoi(int plates, int src, int dst);

hanoi(2,1,2);
```

그리고 나서 1번 장대에 혼자 남아있는 3번 원판을 3번 장대로 옮겨주었다.

```cpp
move(src,dst);
```

남은 1번, 2번 원판을 2번 장대에서 3번 장대로 옮겨주었다. 

```cpp
hanoi(int plates, int src, int dst);

hanoi(2,2,3);
```

정리하면, 3 개의 원판을 1번 장대에서 3번 장대로 옮기는 문제는 

```cpp
hanoi(int plates, int src, int dst);

hanoi(3,1,3) = hanoi(2,1,2) + move(src,dst) +  hanoi(2,2,3);

```

세 파트로 나눌 수 있다. 

1. (시작) 두 개의 원판을 옮기는 문제 (1→2)
2. 하나의 원판을 옮기기  (1 → 3)
3. (종료) 두 개의 원판을 옮기는 문제 (2→3)

각 재귀함수가 출발하고 도착하는 장대가 다르기 때문에, 우리는 출발지와 도착지 외에 남아있는 하나의 장대의 정보도 함께 알고 있어야 한다. 

일반화하면,

```cpp
hanoi(int plates, int src, int dst, int via)//src : 출발, dst : 도착, via : 경유 

= hanoi(plates-1, src, via, dst) + move(src,dst) + hanoi(plates-1, via, dst, src)

```

이제 우리는 이를 코드로 나타낼 수 있다. 

```cpp
int move(int src, int dst){
	cout << src << " " << dst << endl;
	return 1;
}

int hanoi(int plates,int src, int dst, int via){
    if(plates==1){
        move(src,dst);
    }
    else{
					int result = hanoi(plates-1, src, via, dst);
							result += move(src, dst);
				      result += hanoi(plates-1, via, dst, src);
        
				return result;
    }
}

```

해당 코드의 실행 결과는 다음과 같다. 

![hanoi9](https://user-images.githubusercontent.com/55180768/103296498-8af78280-4a39-11eb-9c1d-fcbef2ad34c5.png)

위의 그림과 비교해보면, 순서에 맞게 동작한 것을 볼 수 있다.
