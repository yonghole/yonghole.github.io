---
title: "TableView를 이용한 iOS 앱 만들기 실습"
date: 2021-02-09 01:35:08
categories: iOS
---

# TableView를 이용한 앱 만들기 실습

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

### 2. 스토리보드와 ViewController 연결하기

MVC 디자인 패턴에 따라 DataSource는 Model 역할을 맡습니다. DataSource는 TableView를 생성하고 수정하는데 필요한 정보를 제공합니다. DataSource는 UITableView 객체에 섹션의 수와 행의 수를 알려줍니다. UITableViewDataSource의 필수 메서드는 다음과 같습니다. 

```swift
// TableView 가 몇 개의 Cell을 가지는 지를 반환합니다. 
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int)

// 테이블 뷰에 표시될 cell에 대한 설명 (cell 객체 반환)
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)
```

Delegate는 현재 TableView의 Controller 역할을 맡습니다. TableView의 모양과 수정, 선택 관리 등을 책임집니다. UITableViewDelegate는 필수 메서드는 없지만, 다음과 같은 메서드들을 가지고 있습니다. 

```swift

 func tableView(_ tableView: UITableView, heightForRowAt: IndexPath)
 
 func tableView(_ tableView: UITableView, indentationLevelForRowAt: IndexPath)

 // 행이 선택 되었을 때 호출되는 메서드
 func tableView(_ tableView: UITableView, didSelectRowAt: IndexPath)

 // 행의 선택이 해제되었을 때 호출되는 메서드
 func tableView(_ tableView: UITableView, didDeselectRowAt: IndexPath)

 func tableView(_ tableView: UITableView, viewForHeaderInSection: Int)

 func tableView(_ tableView: UITableView, viewForFooterInSection: Int)

 func tableView(_ tableView: UITableView, heightForHeaderInSection: Int)

 func tableView(_ tableView: UITableView, heightForFooterInSection: Int)

 func tableView(_ tableView: UITableView, willBeginEditingRowAt: IndexPath)

 func tableView(_tableView: UITableView, didEndEditingRowAt: IndexPath?)
```

TableView를 사용하기 위해서는 DataSource의 필수 메서드 두 개(행의 개수 반환 & cell의 구성 반환)가 반드시 구현되어야 합니다. 또한, 해당 함수를 구현하고 있는 ViewController와 현재 TableView를 연결하여 해당 ViewController가 TableView의 dataSource와 Delegate를 책임진다는 것을 알려줘야 합니다. 

ViewController와 TableView를 연결하는 방법에는 두 가지가 있습니다. 

1. 스토리보드의 referencing outlet을 이용하는 방법

![Untitled 7](https://user-images.githubusercontent.com/55180768/107251103-71ede280-6a77-11eb-86a1-e37fc1cb5c45.png)

(코드 내용은 무시하셔도 됩니다.)

ViewController 의 Connections를 보면, Referencing Outlet을 연결할 수 있습니다. 

Referencing Outlet을 스토리보드로 드래그하여 dataSource와 delegate를 연결할 수 있습니다. 

2. ViewController 내 코드로 연결하는 방법

우선 ViewController 내에 TableView 객체를 만들어 주고, 스토리보드의 TableView와 연결해야 합니다. 

우선 다음 코드로 ViewController 내에 tableView 객체를 만들어줍니다. 

```swift
@IBOutlet weak var tableView: UITableView!

```

그 뒤, 해당 Outlet과 TableView를 연결해줍니다.


![Untitled 8](https://user-images.githubusercontent.com/55180768/107251272-8205c200-6a77-11eb-973a-0bc295e66a1a.png)

(코드 내용은 무시하셔도 됩니다.)

viewDidLoad 함수는 view controller가 메모리에 load된 직후 호출됩니다. 따라서 ViewController가 load 된 뒤 TableView의 delegate와 dataSource를 self(ViewController)로 연결하도록 합니다. 


<img width="429" alt="_2021-02-08__5 38 54" src="https://user-images.githubusercontent.com/55180768/107250709-5387e700-6a77-11eb-8e37-fe6b04a03cca.png">

### 3. UITableViewDataSource를 통해 cell 정의하기

방금 전, DataSource는 TableView에 필요한 섹션 수와 행의 수를 알려주며 필수로 구현해야 하는 메서드가 있다고 말씀드렸습니다. 

```swift
// TableView 가 몇 개의 Cell을 가지는 지를 반환합니다. 
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int)

// 테이블 뷰에 표시될 cell에 대한 설명 (cell 객체 반환)
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)
```

이 두 메서드는 옵셔널이 아니기 때문에 UITableViewDataSource 프로토콜을 이용하기 위해서는 반드시 구현되어야 합니다.

ViewController 클래스의 UITableViewDataSource, UITableViewDelegate 두 개의 프로토콜을 추가하면 다음과 같은 에러 메세지가 발생하는 것을 볼 수 있습니다. 필수로 구현해야 하는 메서드를 구현하지 않았기에 발생하는 에러입니다. 위의 메서드들을 직접 타이핑하여 입력하여도 되지만, 간단히 Fix 버튼을 통해 메서드들을 불러줍니다. 


![_2021-02-08__11 37 07](https://user-images.githubusercontent.com/55180768/107250714-54207d80-6a77-11eb-894e-ebda604aac64.png)

두 개의 함수가 로드 되었습니다. 

첫 번째 함수는 위에서 보았던 대로 몇 개의 Cell을 가질 것인지 반환하는 함수로, Int를 반환하도록 되어 있습니다. 

두 번째 함수는 TableView에 표시될 cell에 대해 설명하는 함수로, 반환형이 UITableViewCell이며, 이를 통해 cell 객체를 반환하여 TableView에 사용될 Cell을 반환하도록 합니다. 

![_2021-02-08__11 38 44](https://user-images.githubusercontent.com/55180768/107250723-54b91400-6a77-11eb-9844-63a594f63a8f.png)

우선 첫 번째 함수는 TableView가 몇 개의 cell을 return 할 것인지에 대해 얘기하고 있으니, 간단하게 3을 반환하여봅니다. 

![_2021-02-08__11 59 09](https://user-images.githubusercontent.com/55180768/107250734-5551aa80-6a77-11eb-94a3-4c2159342200.png)

두 번째 함수는 Cell의 형태에 대해 얘기하고 있는데, UITableViewCell을 반환한다고만 나와있기 때문에 조금 더 자세한 정보를 얻기 위해 Apple에서 제공하는 개발자 문서를 살펴보겠습니다. 

![_2021-02-09__12 01 24](https://user-images.githubusercontent.com/55180768/107250780-584c9b00-6a77-11eb-9957-ecfe20b696ec.png)

우선, 우리는 cell의 style이 custom으로 되어 있으며, view를 추가했고 constraints(auto layout)도 추가했습니다. 이제 남은 일은 

- Assign a nonempty string to the cell's identifier attribute.
- Specify the class of custom cells in the Identify inspector.

이 두 가지 입니다. 

첫 번째부터 보겠습니다. 

cell의 identifier attribute에 string을 할당하라고 합니다. 

스토리보드로 가서 cell의 attribute를 살펴보겠습니다. 

![Untitled 9](https://user-images.githubusercontent.com/55180768/107251297-8af69380-6a77-11eb-8ca8-1ba887b0ac50.png)

Cell 의 style은 custom으로 잘 설정되어 있지만, Identifier는 empty인 상태입니다. 따라서 Identifier를 설정해주겠습니다. 

![_2021-02-09__12 10 04](https://user-images.githubusercontent.com/55180768/107250794-597dc800-6a77-11eb-9348-4785d1b9036e.png)

Identifier는 cell로 설정하였습니다. 여기에는 아무 이름이나 들어가도 됩니다. 

그렇다면 과연 Reuse Identifier는 어떤 것이기에 우리가 꼭 할당해주어야 하는걸까요?

애플 개발자 문서에서는, Reuse Identifier에 대해 다음과 같이 설명하고 있습니다. 


![_2021-02-09__12 14 28](https://user-images.githubusercontent.com/55180768/107250801-5a165e80-6a77-11eb-9f98-7426b3858000.png)

Reuse Identifier는 우리 table의 cell들의 creation과 recycling을 용이하게 한다고 합니다. 

이를 위해서 한 가지 알아야 할 것은, 우리가 TableView에서 사용하는 cell들이 무한정 생성되지 않는 다는 것입니다. 

우리가 많이 사용하는 카카오톡을 떠올려보겠습니다. 카카오톡의 친구 목록, 혹은 채팅방 목록도 지금 우리가 공부하고 있는 TableView의 형태를 띄고 있습니다. 카카오톡에서 채팅방 목록이나 친구 목록을 아래로 스크롤하면, 위에 있던 목록은 화면 위로 사라집니다. 이 때 위로 사라진 목록(Cell)은 그대로 있는 것이 아니라, 다른 정보를 담고 아래서 다시 나타나게 됩니다. 즉, 한 화면에 보여질 수 있는 cell의 개수는 제한되어 있기 때문에 cell을 무한정으로 생성하지 않고 화면 밖으로 사라지는 cell을 재활용하여 사용함으로써 메모리 사용을 최소화하고 성능을 개선하게 됩니다. 

우리는 스토리보드에서 TableViewCell의 reuse identifier를 "cell" 로 설정하였습니다. 따라서 우리의 앱이 실행될 때, TableView는 "cell" 이라는 identifier를 가지는 cell들을 queue에 보관합니다. 한 화면에 여러 개의 TableView가 있는 경우에도, identifier를 통해 queue를 구분하고 각 TableView에 맞는 cell을 사용할 수 있게 됩니다. 

이제 두 번째를 보겠습니다. 

- Specify the class of custom cells in the Identify inspector.

우리가 사용할 custom cell의 class를 특정해야 한다고 합니다. 이 때 class는 UITableViewCell의 subclass여야 한다고도 나와있습니다. 개발자문서에 나와있는대로, custom cell을 위한 class를 정의해보겠습니다. 

![_2021-02-09__12 56 03](https://user-images.githubusercontent.com/55180768/107250811-5aaef500-6a77-11eb-8d6c-96f54a156cca.png)

Class의 이름은 ListCell로 하였습니다. Class는 UITableViewCell의 subclass여야 합니다. 

Class를 만들었으니, Identify inspector에서 우리 cell의 class를 명시해야 합니다. 

![Untitled 10](https://user-images.githubusercontent.com/55180768/107251309-8f22b100-6a77-11eb-8fd9-5f6b8badb08f.png)

현재는 cell의 Class 가 UITableViewCell로 되어 있습니다. 

이제 우리가 방금 전 정의했던 custom class의 이름을 입력해줍니다. 


![_2021-02-09__1 08 49](https://user-images.githubusercontent.com/55180768/107250746-55ea4100-6a77-11eb-9221-d8d293ac1192.png)

추가적으로, TableView의 Size tab에서 Row의 높이를 200으로 설정하였습니다. 

여기까지 진행하셨다면, 실행을 통해 우리의 custom cell이 잘 나타나는지 살펴보겠습니다. 

![_2021-02-09__1 11 35](https://user-images.githubusercontent.com/55180768/107250751-5682d780-6a77-11eb-8b47-e3038cd7fe69.png)

아직도 잘 나타나지 않습니다. 

우리는 Cell을 사용할 준비만 했을 뿐, TableView에게 우리가 만든 Custom Cell을 사용하라고 알려주지 않았기 때문입니다. TableView에게 우리가 만든 Custom cell을 사용하라고 알려주기 위해서, 우리는 UITableViewDataSource 의 필수 메서드 중 두 번째 메서드를 마저 구현해야 합니다.

### 4. TableView에게 Custom Cell을 사용하도록 하기

위에서 설명했던 Cell의 재사용을 위해, TableView는 dequeueReusableCellWithIdentifier라는 메서드를 사용합니다. 

![_2021-02-09__1 17 49](https://user-images.githubusercontent.com/55180768/107250757-571b6e00-6a77-11eb-8cf0-572777d77c70.png)

이 메서드는 UITableViewCell class의 객체를 반환해야 하기 때문에, 우선 옵셔널로 우리의 custom class 객체를 생성해주겠습니다. 


![_2021-02-09__1 20 07](https://user-images.githubusercontent.com/55180768/107250765-571b6e00-6a77-11eb-8146-3533d8897933.png)

Identifier에는 우리가 미리 설정했던 Reuse Identifier를 적어줍니다. index Path 는 Cell이 몇 번째에 위치하는지를 나타내는 매개변수입니다. 옵셔널이기 때문에, else문을 통해 UITableViewCell을 반환하도록 하였습니다. 

이제 우리는 개발자문서에서 custom cell을 사용하는 경우에 우리가 구현하도록 요구한 모든 사항을 만족하였습니다. 실행을 통해 결과를 살펴보겠습니다. 

![_2021-02-09__1 23 05](https://user-images.githubusercontent.com/55180768/107250772-57b40480-6a77-11eb-98b5-8cbff5c61329.png)

Custom Cell이 우리의 의도대로 적용된 것을 확인할 수 있습니다.

다음 포스팅에서는 우리의 custom cell에 데이터를 담는 방법을 알아보겠습니다.


Reference : 
[네이버 부스트코스 > iOS 앱 프로그래밍](https://www.boostcourse.org/mo326/joinLectures/12966)
[Apple Developer Documentation](https://developer.apple.com/documentation/)
