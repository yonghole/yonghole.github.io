---
title: "[Git] git에 프로젝트 올리기"
date: 2021-03-13 05:53:36
categories: Git
---

매일 하다가도 오랜만에 하면 까먹는 경우가 있어 스스로 블로그를 보고 참고하기 위해 만든다. 


![image](https://user-images.githubusercontent.com/55180768/110994957-edb3b580-83bc-11eb-9fe8-aee81db812fd.png)


git에 레포지토리를 새로 만든다. 가장 하단에 보면 기본 브랜치가 main으로 정해져있다는 것을 알 수 있다. 기억해놓자. 


![image](https://user-images.githubusercontent.com/55180768/110995202-47b47b00-83bd-11eb-9ffd-172147c82786.png)

레포지토리 주소를 복사한다. 

![image](https://user-images.githubusercontent.com/55180768/110993445-a6c4c080-83ba-11eb-9217-f18b69797afa.png)

레포지토리에 추가하려는 프로젝트가 있는 폴더로 이동한다. 

다음 명령어들을 순서대로 입력한다. 

git remote add origin [자신의 레포지토리 주소]


```shell
  git init
  git remote add origin https://github.com/yonghole/gitTest.git
  git fetch
  git checkout main
  git add .
  git commit -m"test"
  git push origin main

```


중간에 git fetch 후 checkout main을 해주는 이유는 [error: src refspec main does not match any 오류 해결하기](https://yonghole.github.io/git/gitError/)를 참고하면 된다.

![image](https://user-images.githubusercontent.com/55180768/110996976-12f5f300-83c0-11eb-838a-f049f6050988.png)

프로젝트가 잘 올라간 것을 확인할 수 있다. 


