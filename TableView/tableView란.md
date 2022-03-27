<img src ="https://images.velog.io/images/jangdev/post/6ac4a22e-2a8e-41e1-af54-e761576ad842/image.png">

테이블뷰는 iOS 애플리케이션에서 많이 활용하는 사용자 인터페이스이다. 
테이블뷰는 리스트 형태를 지니고 있고, 스크롤이 가능해 많은 정보를 보여 줄 수 있다. 

애플 [TableView](https://developer.apple.com/documentation/uikit/uitableview)에 대한 설명을 보면 A view that presents data using rows in a single column이라고 하는데, 뜻을 해석하면 **하나의 열의 행을 사용해 데이터를 표시하는 View** 라고 한다.

<img src ="https://images.velog.io/images/jangdev/post/a2f4ee3d-8762-43ba-b8dc-495de61c50ab/image.png" width ="300x">


TableView는 위에 그림처럼 하나의 열을 수직으로 스크롤되는 내용의 행을 표시한다.

연락처 앱은 각 연락처의 이름을 행에 표시한고, 하나의 긴 행 목록을 표시하도록 테이블을 구성하고 있다.

설정 앱의 기본 페이지에는 사용 가능한 설정 그룹이 표시된다. 

<img src ="https://images.velog.io/images/jangdev/post/711866ac-ae77-4d5d-9313-a42927e50c12/image.png">

<img src ="https://images.velog.io/images/jangdev/post/95bfb98b-a80b-46dc-aba9-76781013ef0f/image.png">

관련 있는 행을 섹션으로 그룹화하여 내용을 쉽게 탐색할 수 있다.

위에 처럼 tableView는 하나 이상의 섹션을 가질 수 있고, 개별 섹션에는 하나 이상의 Cell이 포함되거나, 포함되지 않을 수 있다.

설정 앱을 보면 첫 번째 섹션에는 하나의 Cell을 가지고 있고, 두 번째 섹션에는 세개의 Cell, 세 번째는 하나의 Cell, 네 번째는 여덟개의 Cell을 가지고 있다.

tableView는 Section과 Cell을 2차원 배열로 관리한다.

Cell의 위치는 Section Index + Cell(row) Index로 표현한다.

## Maps의 Cell Index는 4일까? 

아니다.

배열로 관리하기에 0부터 시작하기 때문에 3이다.

Secion Index또한 0부터 시작한다.

<img src ="https://images.velog.io/images/jangdev/post/d4d9b6cd-d298-45b5-8960-64ec901ec357/image.png">


## **참고**

https://developer.apple.com/documentation/uikit/uitableview