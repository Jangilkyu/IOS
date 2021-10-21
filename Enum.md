## Enum

하나의 주제로 관련된 값의 그룹에 ‘공통 타입’ 을 정의하여 이 값들을 코드에서 '타입-안전한 (type-safe)' 방식으로 작업할 수 있게 해준다.

열거형에서 데이터들은 열거형 객체를 정의하는 시점에 함께 정의되기 때문에 데이터를 함부로 삭제하거나 변경할 수 없다.

변경이나 삭제를 하기 위해서는 객체를 정의하는 구문을 직접 수정해야한다.

열거형의 데이터 멤버들은 '정의(Definition)개념으로 작성되기 때문에 타입으로 사용할 수 있고, 컴파일러가 에러를 미리 알 수 있다.

## Enum Syntax

열거형 객체를 정의할 때는 `enum`키워드를 사용한다. 

열거형을 정의할 객체 이름을 작성하고, 열거형에 내용을 정의하기 위한 중괄호 블록이 추가된다.

중괄호 내에 데이터 멤버들이 `case`키워드로 함께 정의된다.

s
```swift
    enum 열거형이름 {
        case 멤버값1
        case 멤버값2
        case 멤버값3
    }
```


```swift
    enum CompassPoint {
    case north
    case south
    case east, west
    }
```
CompassPoint객체에 north와 south처럼 멤버를 각 줄마다 `case` 구문으로 선언할 수 도 있고, east,west처럼 한꺼번에 선언을 해도 된다.

멤버가 많으면 가독성이 안좋아 질 수 있기때문에 `case`로 나누어서 작성하는 것을 지향한다.

## **열거형 객체의 사용**

- **열거형 타입을 생략할 수 있을때와, 생략할 수 없을때**
    - 1. 열거형 타입으로 정의된 변수에는 열거형 타입명을 생략하고 멤버값만 대입해도 오류가 발생하지 않는다
    - 2. 변수나 상수의 타입 어노테이션을 명시한 경우에는 선언과 동시에 초기화할때 타입명을 생략하고 멤버값만 대입해도 된다.
    - 3. 타입어노테이션 없이 변수나 상수를 초기화 시 타입명을 생략할 수 없다.

열거형의 멤버를 사용하여 변수나 상수에 대입 시 선언되는 변수나 상수는 열거형 타입의 값으로 선언된다.

열거형을 정의하는 것은 새로운 타입의 데이터를 정의하는 것과 같다.

```swift
    let N = CompassPoint.north
    let W = CompassPoint.west
    let S = CompassPoint.south
    let E = CompassPoint.east
````

타입 어노테이션을 명시하지 않더라도 데이터 타입 추론 메커니즘에 의하여 N,W,S,E의 상수들은 CompassPoint타입으로 정의된다.

```swift
    var compassPointToHead: CompassPoint = CompassPoint.north
```

타입 어노테이션을 선언하면 위와 같이 작성할 수 있다. 타입 어노테이션을 선언하면 `CompassPoint`열거형 타입에 정의된 다른 멤버들만 대입할 수 있다.

compassPointToHead 변수의 값을 변경 시 열거형 타입을 생락하고 멤버값만 대입할 수 있다. 이때, 멤버값이 문자열이 아닌 열거형 타입에 속한 값이라는 것을 표시하기 위해 `.(dot)`을 붙여야한다.

```swift
    compassPointToHead = .east
```

위에는 CompassPoint타입으로 정의된 compassPointToHead변수의 값을 변경할때 열거형 타입명을 생략하고 멤버값만 사용하고 있다.

`.east`로 사용할 수 있는 이유는 compassPointToHead 변수가 CompassPoint타입으로 정의되어 있는 것을 컴파일러가 알고 있기 때문이다.

## **switch 구문과 열거형**

```swift
    var compassPointToHead = CompassPoint.west

    switch dirctionToHead {   
        case CompassPoint.north :
        print("북쪽입니다.")
        case CompassPoint.south :
            print("남쪽입니다.")
        case CompassPoint.east :
            print("동쪽입니다.")
        case CompassPoint.west :
            print("서쪽입니다.")
    }
```

**Associated Values (결합 값)**

`결합 값`은 'case 값' 들과 나란히 다른 타입의 값을 저장할 수 있다면 유용할 때가 있다.

'재고 추적 시스템' 이 서로 다른 두 타입의 바코드로 물품을 추적할 필요가 있다고 가정하자.

![image](https://user-images.githubusercontent.com/69107255/137584963-f373c50c-c10e-4865-b24b-70db4c33fc2f.png)

어떤 물품은 `0 에서 9 까지의 숫자를 사용하는, UPC 양식의 1-차원 바코드로 이름표`를 붙인다. 각 바코드는 한 자리 수의 '시스템 코드' 뒤에, 다섯 자리의 '제조회사 코드' 와 다섯 자리의 '물품 코드' 를 가진다. 그 뒤에는 코드를 올바르게 '스캔 (scan)' 했는지를 증명하기 위한 '검사 자리' 가 있다.

![image](https://user-images.githubusercontent.com/69107255/137584966-8b938ec0-367f-4a21-b740-2cb09840e39d.png)

다른 제품은 어떤 'ISO 8859-1' 문자도 사용할 수 있고 최대 '2,953'개 길이의 문자열을 '부호화 (encoding)' 할 수 있는, QR 코드 양식의 2-차원 바코드로 이름표를 붙인다.

```swift
    enum Barcode {
        case upc(Int, Int, Int, Int)
        case qrCode(String)
    }
```

- 결합 값이 `(Int, Int, Int, Int) 타입`인 upc 값 
- 또는 결합 값이 `String 타입`인 qrCode 값

위에 Barcode 라는 열거체 타입은 어느 타입이든 다 되는 '물품 바코드' 를 정의한 열거체는 다음과 같이 정의할 수 있다.

```swift
    var productBarcode = Barcode.upc(8, 85909, 51226, 3)
```

위 코드는 productBarcode 라는 새로운 변수를 생성한 다음 `(8, 85909, 51226, 3)` 라는 튜플 **'결합 값'** 을 가진 `Barcode.upc 값`을 할당한다.

```swift
    productBarcode = .qrCode( "ABCDEFGHIJKLMNOP")
```

위 코드도 productBarcode 변수에 `("ABCDEFGHIJKLMNOP")` 값을 할당한다.


**switch 문 에서 '결합 값' 을 뽑아내기**

각 `결합 값`은 **switch 문의 case 절** 본문에서 사용하기 위해 `상수(let)` 또는 `변수(var)`로 뽑아낸다.

```swift
    switch productBarcode {
        case .upc(let numberSystem, let manufacturer, let product, let check):
            print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).")
        case .qrCode(let productCode):
            print("QR code: \(productCode).")
    }
```

`열거체 case 값`의 `결합 값` 모두를 상수로 뽑아내거나, 변수로 뽑아내려면, 간결하게, 'case 값' 이름 앞에 `단일 var` 또는 `let 보조 설명 (annotation)` 을 붙일 수 있다.

```swift
    switch productBarcode {
        case let .upc(numberSystem, manufacturer, product, check):
            print("UPC : \(numberSystem), \(manufacturer), \(product), \(check).")
        case let .qrCode(productCode):
            print("QR code: \(productCode).")
    }
```

