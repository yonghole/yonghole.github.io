---
title: "[Windows]VS Code에서 C/C++ 컴파일 환경 설정하기"
date: 2020-12-31 14:12:13
categories: etc
comment : true
---


# VScode C++ 컴파일

Visual Studio Code 는 Microsoft 에서 만든 무료 오픈소스 코드 에디터 입니다.

윈도우, 리눅스, 맥에서 모두 사용이 가능합니다. 
![Untitled](https://user-images.githubusercontent.com/55180768/103395626-65ba5f80-4b72-11eb-875f-d9ab9bdf469e.png)

원래는 맥 환경에서는  xcode를, 윈도우에서는 visual studio 2019를 사용했는데, html, css를 새로 공부하려고 처음 코드 에디터를 사용하게 되었습니다. 그러던 중 간편하게  c++ 를 컴파일 할 수 있다는 점을 알게 되어 직접 시도해보았습니다. 

**해당 포스트는 windows 10 환경을 기반으로 작성되었습니다.** 

---

## MinGW 설치하기

VS Code에는 컴파일러가 없습니다. 따라서 C / C++을 컴파일하기 위해 컴파일러를 설치해야 합니다. Windows 환경에서는 MinGW를 설치합니다. 

아래 링크에서 **mingw-get-setup.exe** 파일을 다운로드 합니다.

[MinGW - Minimalist GNU for Windows](https://sourceforge.net/projects/mingw/files/)

다운로드한 exe 파일을 실행합니다. 
![Untitled 1](https://user-images.githubusercontent.com/55180768/103395628-65ba5f80-4b72-11eb-8fac-bfaf172f21e7.png)

Install  버튼을 누릅니다. 

![Untitled 2](https://user-images.githubusercontent.com/55180768/103395629-6652f600-4b72-11eb-86a3-ee94433d1c97.png)

Continue 를 누릅니다. 
![Untitled 3](https://user-images.githubusercontent.com/55180768/103395594-5c30f780-4b72-11eb-87af-b68fb85df344.png)

Continue를 누르면 새로운 창이 뜨게 됩니다. 이 창에서 패키지를 선택해 설치해야 합니다. 

![Untitled 4](https://user-images.githubusercontent.com/55180768/103395596-5d622480-4b72-11eb-86c1-91df48fb8154.png)

패키지에 마우스 오른쪽 버튼을 누르시면 선택 창이 뜨는데, 여기서 ***Mark for Installation***을 선택합니다. 저는 이미 설치가 되어 있기 때문에 표시가 되어있는데, 사진에 표시된 패키지들을 체크해주시면 됩니다. 

![Untitled 5](https://user-images.githubusercontent.com/55180768/103395597-5dfabb00-4b72-11eb-83c9-f96575117a00.png)

그리고 Apply Changes를 누르시면 설치가 완료됩니다. 

이후 환경변수를 편집해야 합니다.  윈도우 검색창에 **시스템 환경 변수**를 검색해주세요.

![Untitled 6](https://user-images.githubusercontent.com/55180768/103395598-5dfabb00-4b72-11eb-974d-11bb456a8a92.png)

**고급** 탭에서 **환경 변수**를 선택합니다. 
![Untitled 7](https://user-images.githubusercontent.com/55180768/103395600-5e935180-4b72-11eb-97e2-383aee9a0c1d.png)
![Untitled 8](https://user-images.githubusercontent.com/55180768/103395601-5e935180-4b72-11eb-9312-bb3ad82f469b.png)

**시스템 변수**에서  **Path**를 선택하고 **편집**을 눌러주세요. 

![Untitled 9](https://user-images.githubusercontent.com/55180768/103395602-5f2be800-4b72-11eb-9850-4bad87a336e6.png)

새로 

![Untitled 10](https://user-images.githubusercontent.com/55180768/103395603-5f2be800-4b72-11eb-8f34-2c5b564a5196.png)

새로만들기 >> C:\MinGW\bin 입력 후 확인을 누릅니다. 

여기까지 진행했다면 컴파일러 설치는 완료되었습니다. 

제대로 설치되었는지 확인하고 싶다면, cmd를 실행합니다. 

![Untitled 11](https://user-images.githubusercontent.com/55180768/103395604-5fc47e80-4b72-11eb-8135-8368b3868184.png)

![Untitled 12](https://user-images.githubusercontent.com/55180768/103395605-5fc47e80-4b72-11eb-8bc3-32e0502eeee2.png)

gcc -v, g++ -v 명령어를 입력하여 버전이 출력된다면 제대로 설치가 된 것입니다. 

## 빌드 설정하기

다시 Visual Studio Code로 돌아옵니다. 
![Untitled 13](https://user-images.githubusercontent.com/55180768/103395606-605d1500-4b72-11eb-86af-e47fd6f07a21.png)

왼쪽의 sidebar에서 가장 밑에 있는 extension 아이콘을 누르고, C/C++를 검색하여 설치합니다. 

C/C++ 코드를 식별하고 명령어, 오류 등을 보기 쉽게 색으로 표시해주는 확장 프로그램입니다.
![Untitled 14](https://user-images.githubusercontent.com/55180768/103395607-605d1500-4b72-11eb-8356-ae6139c11f1c.png)

다시 초기 화면으로 돌아와 Open folder를 통해 작업할 디렉토리를 열어줍니다. 

![Untitled 15](https://user-images.githubusercontent.com/55180768/103395609-60f5ab80-4b72-11eb-9354-76150afcfa22.png)

저는 바탕화면에 temp라는 폴더를 생성하고 확인을 눌렀습니다. 

그리고 파일을 열고 코드를 작성합니다. 

![Untitled 16](https://user-images.githubusercontent.com/55180768/103395610-618e4200-4b72-11eb-8423-eb91859c8bc1.png)

상단바에서 Terminal >> Configure Tasks를 선택해주세요. 

![Untitled 17](https://user-images.githubusercontent.com/55180768/103395611-618e4200-4b72-11eb-991e-f0e8302a2afc.png)

![Untitled 18](https://user-images.githubusercontent.com/55180768/103395612-6226d880-4b72-11eb-84f9-c233cea4aa22.png)

저는 이미 설치 되어 있지만,  아무 설정이 되어 있지 않은 경우 

**빌드 작업을 찾을 수 없습니다.** 라는 메세지가 나타나게 됩니다. 새로운 빌드 작업 구성 메뉴를 선택해주세요. 

Create task.json file from template 메뉴를 선택해주시면 됩니다. 

![Untitled 19](https://user-images.githubusercontent.com/55180768/103395613-6226d880-4b72-11eb-8d36-dc2de77dd86d.png)

가장 밑의 Others Example to run an arbitrary external command 를 선택해줍니다. 

![Untitled 20](https://user-images.githubusercontent.com/55180768/103395614-62bf6f00-4b72-11eb-83c6-cef384a7bdb4.png)

다음과 같이 기본 템플릿의 task.json 파일이 생성됩니다. 

task.json 파일의 내용을 아래 내용으로 변경해주세요.

```cpp
{
    "version": "2.0.0",
    "runner": "terminal",
    "type": "shell",
    "echoCommand": true,
    "presentation" : { "reveal": "always" },
    "tasks": [
          //C++ 컴파일
          {
            "label": "save and compile for C++",
            "command": "g++",
            "args": [
                "${file}",
                "-std=c++11",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "group": "build",

           

            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                  
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
        //C 컴파일
        {
            "label": "save and compile for C",
            "command": "gcc",
            "args": [
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "group": "build",

            
            "problemMatcher": {
                "fileLocation": [
                    "relative",
                    "${workspaceRoot}"
                ],
                "pattern": {
                    
                    "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
                    "file": 1,
                    "line": 2,
                    "column": 3,
                    "severity": 4,
                    "message": 5
                }
            }
        },
   
         {
             "label": "execute",
             "command": "cmd",
             "group": "test",
             "args": [
             "/C", "${fileDirname}\\${fileBasenameNoExtension}"
             ]
    
         }
    ]
}
```

이후 단축키 설정만 해주시면 모든 과정이 끝납니다. 
![Untitled 21](https://user-images.githubusercontent.com/55180768/103395615-62bf6f00-4b72-11eb-81df-e2099fe360ed.png)

상단바에서 File >> Preferences >> Keyboard Shortcuts 에 들어갑니다. 

![Untitled 22](https://user-images.githubusercontent.com/55180768/103395616-63580580-4b72-11eb-9930-559782d2a21a.png)

사진에 표시된 버튼을 누르시면 "keybindings.json" 파일이 열립니다. 

![Untitled 23](https://user-images.githubusercontent.com/55180768/103395618-63580580-4b72-11eb-893a-0a812e46ad62.png)

아래 내용을 복사하셔서 [ ] 사이에 붙여넣기 하고 저장해주세요. 

```cpp
	//컴파일
    { "key": "ctrl+alt+c", "command": "workbench.action.tasks.build" },
    
    //실행
    { "key": "ctrl+alt+r", "command": "workbench.action.tasks.test" }
```

이제 탐색기에서 컴파일 할 파일을 선택하고 ctrl +alt + c를 누릅니다. 

![Untitled 24](https://user-images.githubusercontent.com/55180768/103395619-63f09c00-4b72-11eb-9db3-298a67a29ea1.png)

사진 상으로는 cpp 파일이기 때문에 save and compile for C++ 을 선택해주시면 됩니다.

만약 c 파일이라면 save and compile for C를 선택하시면 됩니다. 

코드에 문제가 없다면 다음과 같은 내용이 출력됩니다. 
![Untitled 25](https://user-images.githubusercontent.com/55180768/103395620-63f09c00-4b72-11eb-9862-56dbc76dc1b6.png)

코드에 문제가 있다면 다음처럼 오류 메세지가 출력됩니다. 
![Untitled 26](https://user-images.githubusercontent.com/55180768/103395623-64893280-4b72-11eb-9289-ca74047f8209.png)

이제 컴파일된 코드에 ctrl + alt + r을 누릅니다. 
![Untitled 27](https://user-images.githubusercontent.com/55180768/103395624-6521c900-4b72-11eb-8756-8ec811e66a25.png)

execute 가 뜨면 enter를 눌러줍니다. 

![Untitled 28](https://user-images.githubusercontent.com/55180768/103395625-6521c900-4b72-11eb-89f9-fb9620624d23.png)

결과가 출력되는 것을 볼 수 있습니다. 

---
