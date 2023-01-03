# 5️⃣ 인터페이스 분리 법칙(ISP: Interface Segregation Principle)
- 클라이언트가 불필요한 자신이 사용하지 않는 인터페이스에 의존하지 말아야한다.
- 상속받은 메서드를 퇴화시켜야하는 경우가 발생할 수 있음
- 불필요한 인터페이스에 의존하여 불필요한 빌드가 유발될 수 있음
- 큰 인터페이스를 작은 인터페이스들로 분리하고, 필요한 부분만 클라이언트가 취사선택하여 사용할 수 있게 해야함.

예시를 통해 살펴보자!
```Swift
// ISP 원칙을 위배한 코드

protocol Shape {
    var area: Float { get }
    var length: Float { get }
}

class Square: Shape {
    var width: Float
    var height: Float

    var area: Float {
        return width * height
    }

    // 불필요한 코드
    var length: Float {
        return 0
    }

    init(width: Float, height: Float) {
        self.width = width
        self.height = height
    }
}

class Line: Shape {
    var pointA: Float
    var pointB: Float

    // 불필요한 코드
    var area: Float {
        return 0
    }

    var length: Float {
        return pointA - pointB
    }

    init(pointA: Float, pointB: Float) {
        self.pointA = pointA
        self.pointB = pointB
    }
}
```
Line, Square 모두 Shape 프로토콜을 채택한 객체이지만 실제로 Square는 length라는 변수가   
Line은 area라는 변수가 필요없게 됩니다.   
그럼에도 단지 프로토콜을 채택했다는 이유만으로 필요없는 기능이 구현되고있으므로 ISP에 위배됩니다.   
개선한 코드는 아래와 같습니다.
```Swift
protocol AreaCalculatalbeShape {
    var area: Float { get }
}

protocol LengthCalculatableShape {
    var length: Float { get }
}

class Square: AreaCalculatableShape {
    var width: Float
    var height: Float

    var area: Float {
        return width * height
    }

    init(width: Float, height: Float) {
        self.width = width
        self.height = height
    }
}

class Line: LengthCalculatableShape {
    var pointA: Float
    var pointB: Float

    var length: Float {
        return pointA - pointB
    }

   init(pointA: Float, pointB: Float) {
        self.pointA = pointA
        self.pointB = pointB 
}
```
위와 같이 기존에 필요없는 기능들을 구현하고 있던 인터페이스들을 더욱 세분화하여 나누어주었습니다.   
각각 필요한 프로토콜만 채택하여 ISP원칙을 지키는 프로그램 설계가 되었습니다!
