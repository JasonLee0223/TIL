# 3️⃣ 리스코프 치환 원칙(LSP: Liskov Substitution Principle)
부모(super class)로 동작하는 곳에서 자식(sub class)를 넣어주어도 대체가 가능해야한다는 원칙.   
즉, **`자식 클래스는 부모 클래스로써의 역할을 완벽히 할 수 있어야한다.`**   
풀어서 말한다면 `부모클래스의 타입에 자식 클래스의 인스턴스를 넣어도 똑같이 동작`해야한다.   
요약하면, 자신의 속성을 위해 부모 클래스 기능을 거부 / 퇴화

예시를 보고 이해해보도록 하자!
```Swift
// 잘못된 예시

class Rectangle {
    var width: Float = 0
    var height: Float = 0

    var area: Float {
        return width * height
    }
}

class Square: Rectangle {
    override var width: Float {
        didSet {
            height = width
        }
    }
}

func printArea(of rectangle: Rectangle) {
    rectangle.height = 3
    rectangle.width = 6
    print(rectangle.area)
}

let rectangle = Rectangle()
printArea(of: rectangle)            // 18

let square = Square()
printArea(of: square)               // 36
```
실제로 정사각형은 직사각형이라고 할 수 있다. (범주를 포함하고 있다.)   
이 원리에 따라 프로그램을 설게하면 정사각형의 넓이를 출력할 때, `height = width`라는 구문으로 인해   
printArea(_ : Rectangle)에서 원하는 결과를 얻지 못하게된다.   

즉, 부모(super class)의 역할을 자식(sub class)에서 대신하지 못하고 있는 상황이 발생...   
```Swift
// 좋은 예시

protocol Shape {
    var area: Float { get }
}

class Rectangle: Shape {
    let width: Float
    let height: Float

    var area: Float {
        return width * height
    }

    init(width: Float, height: Float) {
        self.width = width
        self.height = height
    }
}

class Square: Shape {
    let length: Float

    var area: Float {
        return length * length
    }

    init(length: Float) {
        self.length = length
    }
}
```
다음과 같은 방법으로 Shape라는 프로토콜을 채택할 수 있게 설계하고 실제 구현부는 채택하는 하위 클래스로 넘기면   
LSP 원칙에 어긋나지 않고 설계할 수 있게된다.   
즉, `Shape의 역할`을 Square, Rectangle 모두가 `기존 룰을 위반하지않고 동작`하는 프로그램이 구현될 수 있다.   