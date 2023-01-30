# General Conventions 일반적인 규칙

- **O(1) 복잡도가 아닌 연산 프로퍼티는 설명을 만들어라.**   
대부분 사람들은 저장 프로퍼티에 익숙해서 프로퍼티 값에 접근하는 것은 추가적인 비용이 발생한다고 생각하지 않기 때문이다.   

- **소속이 없는 자유로운 함수를 만들기보다는 메서드나 속성을 만들어라.**   
다음의 특별한 경우에만 함수를 고려하라.

1. 명확하게 `self`가 없을 때
   ```Swift
   min(x,y,z)
   ```
2. 제약없는 제네릭 함수인 경우
   ```Swift
   print(x)
   ```
3. 함수 표현이 특정한 도메인 표기법을 준수하는 경우
   ```Swift
   sin(x)
   ```

- **대소문자 표기법을 따른다.**   
  타입이나 프로토콜 이름은 `UpperCamelCase`형태로 사용하고, 그 외에는 모두 `lowerCamelCase`를 사용한다.   
  - 미국식 영어 표현처럼 모두 대문자로 쓰는 두문자(축약어)는 일관되게 대문자나 소문자로 사용하라.   
    ```Swift
    var utf8Bytes: [UTF8.CodeUnit]
    var isRepresentableAsASCII = true
    var userSMTPServer: SecureSMTPServer
    ```

  - 다른 축약어는 일상적인 영어 단어로 표기하라.
    ```Swift
    var radarDetector: RadarScanner
    var enjoysScubaDiving = true
    ```
- 메서드가 같은 의미를 갖고 있거나 특정한 도메인 영역에서만 동작을 하는 경우에는 **기본 이름을 공유할 수 있다.**
  - ✅ 예를 들어, 아래의 메서드들은 동일한 작업을 수행한다.
    ```Swift
    extension Shape {
    /// Returns `true` if `other` is within the area of `self`;
    /// otherwise, `false`.
    func contains(_ other: Point) -> Bool { ... }

    /// Returns `true` if `other` is entirely within the area of `self`;
    /// otherwise, `false`.
    func contains(_ other: Shape) -> Bool { ... }

    /// Returns `true` if `other` is within the area of `self`;
    /// otherwise, `false`.
    func contains(_ other: LineSegment) -> Bool { ... }
    }
    ```
  - ✅ 아래의 기하학 타입과 컬렉션은 별도의 다른 영역이라서, 프로그램 내에서 메서드 이름과 같아도 된다.
    ```Swift
    extension Collection where Element : Equatable {
    /// Returns `true` if `self` contains an element equal to
    /// `sought`; otherwise, `false`.
    func contains(_ sought: Element) -> Bool { ... }
    }
    ```
  - ⛔️ 아래와 같은 `index`메서드는 서로 다른 의미를 갖고 있으므로 다르게 불려야한다.
    ```Swift
    extension Database {
    /// Rebuilds the database's search index
    func index() { ... }

    /// Returns the `n`th row in the given table.
    func index(_ n: Int, inTable: TableID) -> TableRow { ... }
    }
    ```
  - ⛔️ "리턴 타입만 오버로딩"하는 방식은 타입 추론에 혼란을 야기하기 때문에 피해야한다.
    ```Swift
    extension Box {
    /// Returns the `Int` stored in `self`, if any, and
    /// `nil` otherwise.
    func value() -> Int? { ... }

    /// Returns the `String` stored in `self`, if any, and
    /// `nil` otherwise.
    func value() -> String? { ... }
    }
    ```
