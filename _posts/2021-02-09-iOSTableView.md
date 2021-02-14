---
title: "TableView를 이용한 iOS 앱 만들기 실습(Part1)"
date: 2021-02-09 01:35:08
categories: iOS
---

## Auto Layout을 통해 View를 구성하고 Custom cell을 사용하는 TableView 정의하기

![_2021-02-06__10 57 41](https://user-images.githubusercontent.com/55180768/107250510-466af800-6a77-11eb-93e4-174c3c50e0fa.png)

### TableView

데이터를 여러 개의 행으로 표현해주는 layout이다. 

ViewController에 TableView를 추가하고 Table View Cell을 추가하여 사용할 수 있다. 

### 실습 목표 : TableView를 사용한 앱을 만들며 기본적인 iOS앱의 구조를 익힌다.

### 앱 개요: TableView를 이용한 상품 리스트와, 선택 시 상품의 상품 페이지를 Modal로 보여주는 detailView를 이용한다.

### 1. 스토리보드와 Auto Layout을 이용해 앱 디자인 및 구성하기

TableView를 생성하기 위해서 가장 간단한 방법으로 스토리보드에서 커스텀 UITableViewController를 사용하겠습니다. 

![_2021-02-06__11 00 15](https://user-images.githubusercontent.com/55180768/107250567-49fe7f00-6a77-11eb-805a-003f2b47ca6f.png)

처음 Xcode를 열고 iOS App을 선택한 뒤 프로젝트를 열면 다음과 같이 새하얀 스토리보드가 우리를 반겨줍니다. 

이제부터, 이 스토리보드에 우리가 원하는 컴포넌트들을 채워 나가며 앱을 디자인 해보겠습니다. 

![Untitled](https://user-images.githubusercontent.com/55180768/107251329-947ffb80-6a77-11eb-86af-1a370585020e.png)

우선, 스토리보드를 클릭한 상태에서 오른쪽 위 + 버튼을 누르고, TableView를 선택해 스토리보드로 드래그 해줍니다.  드래그 한 스토리보드는 자신이 원하는 사이즈로 조정합니다. 

![Untitled 1](https://user-images.githubusercontent.com/55180768/107250819-5b478b80-6a77-11eb-9823-ec2024dde6af.png)

TableView는 여러 개의 TableViewCell로 구성되어 있기 때문에 TableViewCell을 TableView에 추가해줍니다. 추가된 TableViewCell은 새로운 Cell을 만들고 싶을 때마다 추가해주는 것이 아니고, 해당 TableView에서 사용할 Cell을 대표하게 됩니다. 

![Untitled 2](https://user-images.githubusercontent.com/55180768/107250882-600c3f80-6a77-11eb-8ec8-4ea1a71b0921.png)

이제 화면 내에서 TableView의 위치를 지정해주기 위해 Auto Layout을 사용합니다. Auto Layout으로 화면을 구성하는 방법에는 여러 가지가 있습니다. 정해진 정답은 없기 때문에, 자신이 설정한 constraints 간에 간섭이 일어나는 경우를 제외하고는 자유롭게 화면을 구성해 나갈 수 있습니다. 

Auto Layout을 사용하기 위해 TableView에서 Ctrl 키를 누른 채 Safe Area로 드래그 합니다. 

![Untitled 3](https://user-images.githubusercontent.com/55180768/107250910-63073000-6a77-11eb-9156-f2b071d94af0.png)

나오는 선택 창에서, 저는 화면의 safe area 에 대한 Top, Left (leading), Right (Trainling), Bottom margin을 설정하기로 했습니다. 선택을 마치면 오른쪽에 있는 Size 페이지에 제약들이 추가되고 있는 것이 보입니다. 

![Untitled 4](https://user-images.githubusercontent.com/55180768/107250959-67334d80-6a77-11eb-9694-8e278efca0f9.png)

저는 위와 같이 설정을 변경하였습니다. 화면이 핸드폰에 꽉 차게 느껴지게 만들고 싶었기 때문입니다. 정렬되어 보이게 하기 위해 TableView내의 Cell의 높이는 200으로 고정하려고 합니다. 

아까와 같이 ctrl키를 누른 후, 이번에는 TableViewCell에서 TableViewCell로 드래그해줍니다. 

![Untitled 5](https://user-images.githubusercontent.com/55180768/107251001-6ac6d480-6a77-11eb-8799-c4c39e6cce77.png)

TableView 내의 Cell 하나의 row height는 200으로 고정되었습니다. 

맨 처음 보았던 앱 화면을 참고하여 각 Cell들이 무엇으로 구성될 지 생각해봅니다. 

![_2021-02-06__11 30 28](https://user-images.githubusercontent.com/55180768/107250584-4b2fac00-6a77-11eb-9fd5-b51c00ab7940.png)

각 Cell은 사진 하나와 제목, 지역, 금액 등의 정보를 담고 있습니다. 

![Untitled 6](https://user-images.githubusercontent.com/55180768/107251063-6f8b8880-6a77-11eb-98c3-7b2bb31b6bd3.png)

살펴보면 대략 다음과 같은 구성으로 볼 수 있습니다. TableView와 TableViewCell을 추가했던 방식과 동일하게 해당 컴포넌트들을 TableViewCell에 추가해줍니다. 

![_2021-02-06__11 35 00](https://user-images.githubusercontent.com/55180768/107250602-4c60d900-6a77-11eb-97dd-164a2db7080d.png)

추가한 직후에는 다음과 같은 모습으로 보일 것입니다. 

이제 Auto Layout을 통해 해당 컴포넌트들의 위치와 속성도 정의해야 합니다. 

위에서 TableView 에 적용했던 방식과 동일하게 설정합니다. 

Auto Layout을 적용할 때 가장 중요한 것은, 각 Constraints 간에 충돌이 없도록 하는 것입니다. 

만약 충돌이 일어났거나, 빠진 Constraints가 있다면 다음과 같이 빨간색 화살표로 표시됩니다. 

![_2021-02-06__11 43 19](https://user-images.githubusercontent.com/55180768/107250609-4cf96f80-6a77-11eb-9667-2e2ed2b14d54.png)

가장 밑 라벨의 X 좌표 설정을 모두 삭제했습니다. 이 경우는 Constraints가 빠진 경우에 속하며, 빨간색 화살표를 눌러보면 다음과 같은 설명을 볼 수 있습니다. 

![_2021-02-06__11 44 47](https://user-images.githubusercontent.com/55180768/107250618-4d920600-6a77-11eb-851b-b25073eea58a.png)

다음과 같이 가장 밑의 라벨에 X 좌표에 대한 정보를 추가하면 에러가 사라지는 것을 볼 수 있습니다. 

![_2021-02-06__11 45 16](https://user-images.githubusercontent.com/55180768/107250626-4e2a9c80-6a77-11eb-8b63-a1a31ed41183.png)

Auto Layout은 해당 어플리케이션이 크기가 다른 디바이스들에서 깨지거나 잘못 위치되지 않고 각자의 속성에 따라 자동으로 배치되도록 해줍니다. 따라서 Safe Area를 기준으로 각 컴포넌트들이 어떤 위치에 배치되어야 하는지를 명시해야 합니다.

추가로, AutoLayout을 제대로 익히기 위해서는 스스로 생각하며 layout을 배치해봐야 합니다. 

Table View Cell 내에서 컴포넌트들의 Auto Layout 설정은 다음과 같습니다. 

**UI Image View**

![_2021-02-06__11 49 30](https://user-images.githubusercontent.com/55180768/107250630-4e2a9c80-6a77-11eb-983b-0a668baad560.png)

![_2021-02-06__11 49 38](https://user-images.githubusercontent.com/55180768/107250638-4f5bc980-6a77-11eb-98b2-00f9a24fd529.png)

(위에서부터)

**Label1**

![_2021-02-07__12 13 04](https://user-images.githubusercontent.com/55180768/107250645-4f5bc980-6a77-11eb-9abf-1772c8c0fc8b.png)

![_2021-02-07__12 13 14](https://user-images.githubusercontent.com/55180768/107250651-4ff46000-6a77-11eb-9a66-70cebf7abda0.png)

**Label2**

![_2021-02-07__12 13 27](https://user-images.githubusercontent.com/55180768/107250658-508cf680-6a77-11eb-98b7-d752b1a1ed51.png)

![_2021-02-07__12 13 35](https://user-images.githubusercontent.com/55180768/107250663-51258d00-6a77-11eb-988a-7558089a0b2e.png)

**Label3**

![_2021-02-07__12 13 54](https://user-images.githubusercontent.com/55180768/107250667-51258d00-6a77-11eb-80aa-1361327017b6.png)

![_2021-02-07__12 14 04](https://user-images.githubusercontent.com/55180768/107250674-51be2380-6a77-11eb-9cfa-604e17a6d091.png)

과연, 실제 핸드폰 화면에서도 제대로 배치가 되었는지 시뮬레이터를 통해 확인해보겠습니다.

![_2021-02-07__12 16 13](https://user-images.githubusercontent.com/55180768/107250698-52ef5080-6a77-11eb-83c5-2dbeee4559eb.png)

하나도 반영되어 있지 않습니다. UITableView는 DataSource와 Delegate가 없다면 동작할 수 없기 때문입니다. 


다음 포스팅에서는 StoryBoard와 ViewController를 연결하고, DataSource와 Delegate를 설정해주겠습니다. 

[다음 포스팅](https://yonghole.github.io/ios/iosTableViewPart2/)


Reference : 

[네이버 부스트코스 > iOS 앱 프로그래밍](https://www.boostcourse.org/mo326/joinLectures/12966)

[Apple Developer Documentation](https://developer.apple.com/documentation/)
