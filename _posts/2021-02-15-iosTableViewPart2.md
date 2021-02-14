---
title: "TableView를 이용한 iOS 앱 만들기 실습(Part2)"
date: 2021-02-15 01:35:08
categories: iOS
---

## 2. 스토리보드와 ViewController 연결하기

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

[다음 포스팅](https://yonghole.github.io/ios/iosTableViewPart3/)에서는 우리의 custom cell에 데이터를 담는 방법을 알아보겠습니다.


Reference : 

[네이버 부스트코스 > iOS 앱 프로그래밍](https://www.boostcourse.org/mo326/joinLectures/12966)

[Apple Developer Documentation](https://developer.apple.com/documentation/)
