---
title: "TableView를 이용한 iOS 앱 만들기 실습(Part3)"
date: 2021-02-15 03:35:58
categories: iOS
---

# TableView를 이용한 앱 만들기 실습 3

## Custom Cell에 data를 담기

지난 포스트에서는 TableView를 이용하고, custom cell을 사용하도록 하는 것을 알아보았습니다. 

이번 포스트에서는 custom cell에 실제로 데이터를 담아 TableView를 통해 보여주도록 하겠습니다. 

우선, 지난 포스트에서 만들었던 Custom cell 은 다음과 같습니다. 

![_2021-02-15__1 34 52](https://user-images.githubusercontent.com/55180768/107885674-073d1b00-6f3f-11eb-802a-bc0ad88dcb18.png)

Listcell이라는 이름을 가지는 class로, TableView에 들어가는 cell 타입은 UITableViewCell 클래스를 상속받습니다. 

스토리보드를 통해 구성했던 custom cell은 다음과 같은 요소들을 가지고 있습니다. 

![_2021-02-15__1 36 01](https://user-images.githubusercontent.com/55180768/107885676-0906de80-6f3f-11eb-9e61-3dd68439fe6a.png)


UIImageView, Label, Label,Label 입니다. 

먼저, 스토리보드에 있는 UI컴포넌트들을 ViewController에서 코드로 연결해주어야 합니다. 

따라서 다음과 같이 Outlet을 이용해 연결해주겠습니다. 

먼저 Outlet을 선언해줍니다.

```swift
class Listcell: UITableViewCell{
    @IBOutlet weak var imgView: UIImageView!
    @IBOutlet weak var title:UILabel!
    @IBOutlet weak var location:UILabel!
    @IBOutlet weak var price:UILabel!
    
}
```

이후, 스토리보드의 각 컴포넌트들과 Outlet을 연결해줍니다.

![_2021-02-15__3 09 06(2)](https://user-images.githubusercontent.com/55180768/107885683-0efcbf80-6f3f-11eb-8f7a-89d5fcc2870d.png)


이제, 이 cell이 어떤 데이터를 담을 건지에 대한 정보를 알려줘야 합니다. 

따라서 TableView를 사용하기 위한 UITableViewDataSource 프로토콜의 필수 구현 함수들 중 두 번째

```swift
	func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) ->
 UITableViewCell {

}
```

함수에 cell에 대한 내용을 담아줘야 합니다. 

그 전에, cell 에 담을 데이터를 먼저 준비해야 합니다. 

우리에게 필요한 것은 

1. UIImageView에 들어갈 image
2. Title label에 들어갈 String들
3. 지역 label에 들어갈 지역 String들
4. 가격 label에 들어갈 가격 Int들

입니다. 

데이터는 다음과 같이 List로 구현을 하게 되는데, 사진을 준비합니다. 

이미지는 프로젝트의 Assets.xcassets 내에 담아줘야 합니다. 

![_2021-02-15__2 22 16](https://user-images.githubusercontent.com/55180768/107885677-099f7500-6f3f-11eb-87e5-d5446c64a49b.png)

다음과 같이 이미지 8장을 준비했습니다. 

![_2021-02-15__2 24 32(2)](https://user-images.githubusercontent.com/55180768/107885679-0ad0a200-6f3f-11eb-9080-1ac86cae1a6b.png)

Xcode내의 프로젝트 폴더에서 Assets.xcassets 폴더를 열고 사진을 드래그 해줍니다. 

![_2021-02-15__2 26 42](https://user-images.githubusercontent.com/55180768/107885680-0dcb9280-6f3f-11eb-86ec-a7939b5deb08.png)

다음과 같이 사진이 추가된 것을 볼 수 있습니다. 

이제 Label에 들어갈 data를 준비해야 합니다.  

각각을 Array로 따로 준비해도 되지만, 정보의 가독성을 높히고 관련있는 정보들을 잘 묶어두기 위해 struct를 사용해보겠습니다. 

```swift
struct article{
    let title : String // title label에 사용합니다.
    let location : String // location label에 사용합니다.
    let price : Int // 가격 label에 사용합니다. 
    let recepNum : Int // 연결된 이미지의 제목을 담습니다. 
}
```

recepNum은 연결된 이미지의 제목을 담습니다. 

저는 이미지의 이름들을 각 article의 순서로 정할 것이기 때문에 다음과 같이 Int 형을 사용하였습니다. 

만약 이미지의 이름을 String으로 한다면 다음과 같이 해도 무방합니다.

```swift
struct article{
    let title : String // title label에 사용합니다.
    let location : String // location label에 사용합니다.
    let price : Int // 가격 label에 사용합니다. 
    let imgName : String // 연결된 이미지의 제목을 담습니다. 
}
```

이제 struct를 담는 list를 선언합니다. 

```swift
var articleList :[article] = [article(title: "에어팟2 미개봉 팝니다", location: "신갈동", price: 130000, recepNum: 1 ),
                                  article(title: "아이패드 팝니다", location: "이매동", price: 600000, recepNum: 2),
                                  article(title: "고양이 보여드립니다", location: "이매동", price: 100000, recepNum: 3),article(title: "고양이 있습니다.", location: "우만동", price: 300, recepNum: 4),
                                  article(title: "맥북에어 미개봉 팝니다", location: "상현동", price: 1200000, recepNum: 5),
                                  article(title: "공기청정기 팝니다", location: "신갈동", price: 90000, recepNum: 6),
                                  article(title: "고양이 자랑합니다", location: "???", price: 999999, recepNum: 7),
                                  article(title: "대게 판매합니다", location: "이매동", price: 50000, recepNum: 8)]
    var contextList :[String] = ["한 번도 사용하지 않은 에어팟 입니다. 진짜 그냥 새 것입니다.",
    "포장만 뜯은 아이패드 입니다. 급처합니다. 아주대 근처 직거래",
    "두 번 쓰다듬고 꾹꾹이 한 번 포함 가격입니다.",
    "지나가다 한 번 쳐다보는 가격입니다. 특징으로는 귀엽습니다.",
    "맥북에어 미개봉입니다. 진짜 미개봉입니다. 겉포장까지 팝니다.",
    "공기청정기 입니다. 공기가 맑아지는 효과가 있습니다. 깔깔",
    "고양이 입니다. 다현 닮은 고양이로 유명합니다. 다른 각도에서 찍은 짤 자랑합니다.",
    "대게입니다. 방금 쪄서 뜨겁습니다."
    ]
```

데이터가 모두 준비되었으니 이제 cell에 데이터를 담아보도록 하겠습니다. 

우선 몇 개의 cell을 보여줄 것인지를 알려줘야 합니다. 

우리는 여덟 개의 cell을 준비했기 때문에 직접 8을 적어 반환하도록 해도 되지만, 데이터 리스트의 사이즈 만큼 cell을 만들면 되기 때문에 추후에 데이터를 추가하거나 삭제할 경우를 대비해 후자로 적어줍니다. 

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return articleList.count
    }
```

이제 cell에 데이터를 담아 줘야 합니다. 

cell에 데이터를 담을 때는 이전 포스트에서 구현했던 함수에 내용을 채워주면 됩니다. 

각 컴포넌트에 맞는 데이터를 연결해주도록 하겠습니다. 

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
        if let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as? Listcell {
            let tmp = articleList[indexPath.row]
            let img = UIImage(named: "\(tmp.recepNum).jpg")
            cell.imgView.image = img
            cell.title.text = tmp.title
            cell.location.text = tmp.location
            cell.price.text = "\(tmp.price)"
            return cell
        }else{
            return UITableViewCell()
        }
    }
```

제대로 cell이 반환되는지 확인하기 위해 실행해보겠습니다. 

![_2021-02-15__3 12 02](https://user-images.githubusercontent.com/55180768/107885685-0f955600-6f3f-11eb-93c6-c7290eae5a44.png)

정상적으로 cell에 데이터가 담긴 것을 볼 수 있습니다. 

다만, Title의 폰트 사이즈가 너무 커서 살짝 잘리니, 폰트의 사이즈를 줄여줍니다. 

![_2021-02-15__3 14 10](https://user-images.githubusercontent.com/55180768/107885687-102dec80-6f3f-11eb-8d83-229f2f9e049a.png)

다음 포스팅에서는 cell을 선택했을 때 새로운 View를 띄우고, ViewController 간에 데이터를 주고 받는 방법을 알아보겠습니다.

Reference : 

[네이버 부스트코스 > iOS 앱 프로그래밍](https://www.boostcourse.org/mo326/joinLectures/12966)

[Apple Developer Documentation](https://developer.apple.com/documentation/)
