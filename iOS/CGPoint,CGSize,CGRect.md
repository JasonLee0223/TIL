# CGPoint, CGSize, CGRect

## View의 위치와 크기를 결정하는 방법
처음 View를 넣으려고 할 때 단순하게 `View를 어디에 위치시켜서 얼만큼의 크기로 만들까?`라는 질문이 생각난다.   
그러면 `위치(Point)`와 `크기(Size)`를 구성할 수 있도록 해야한다.   
- 위치   
View의 시작위치를 알기 위한 `(x, y) 좌표`가 필요하고 이 좌표는 iOS View `기준점인 왼쪽 꼭대기 (0, 0)`으로부터 시작한다.
- 크기   
이제 위치를 알았으니 얼만큼의 Size를 같는 뷰를 그릴 것인지 (width, height)가 필요하다.

이렇게 기본적으로 View를 그리기위해서는 `총 4가지 (x, y), (width, height)가 필수적`이다.

## 1. (x, y) 좌표를 설정하는 CGPoint
```Swift
public struct CGPoint {
    public var x: CGFloat
    public var y: CGFloat
    public init()
    public init(x: CGFloat, y: CGFloat)
}

// Example
let position: CGPoint = .init(x: 100, y: 100)
```
여기서 중요한 부분은 CGPoint의 x,y는 `Float 변수`를 사용한다.
따라서 View의 위치를 나타낼 땐 이 CGPoint를 이용한다.

## 2. (width, height) Size를 설정하는 CGSize
```Swift
public struct CGSize {
    public var width: CGFloat
    public var height: CGFloat
    public init()
    public init(width: CGFloat, height: CGFloat)
}

// Example
let mySize: CGSize = .init(width: 200, height: 300)
```
여기까지 오게되면 View를 그리는 요소에 대한 파악은 끝났다.
그런데 실제로 UIView를 초기화하려면
```Swift
let myView: UIView = .init(frame: CGRect)
```
위와 같이 정의되며 CGPoint와 CGSize를 정의하지않고 CGRect를 정의하라고 요구한다.

## 3. CGSize + CGPoint = CGRect
```Swift
public struct CGRect {
    public var origin: CGPoint
    public var size: CGSize
    public init()
    public init(origin: CGPoint, size: CGSize)
}

// Exmaple
let myRect: CGRect = .init(origin: CGPoint(x: 100, y: 200), size: CGSize(width: 150, height:200) )
let myRect: .init(x: 100, y: 200, width: 150, height: 200)

let myView: UIView = .init(frame: myRect)
```
- origin: `CGPoint`타입의 변수   
- size: `CGSize`타입의 변수   
따라서 View를 그릴 때는 origin = (x,y) & size = (width, height)를 명시해주면 그릴 수 있게 되는 것이다.

### 참고사이트 🌐
[iOS) CGPoint, CGSize, CGRect](https://babbab2.tistory.com/42)  
[CGPoint | Apple Developer Documentation](https://developer.apple.com/documentation/corefoundation/cgpoint)   
[CGSize | Apple Developer Documentation](https://developer.apple.com/documentation/corefoundation/cgsize)   
[CGRect | Apple Developer Documentation](https://developer.apple.com/documentation/corefoundation/cgrect)   