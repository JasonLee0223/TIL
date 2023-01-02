# SOLID

1. 단일 책임 원칙(SRP: Single-Responsibility Principle)
   - 한 타입은 단 한가지의 책임만을 가져야한다.   
    책임은 변경의 이유야.    

    - 우리는 높은 응집도로 낮은 결합도를 갖게 해야한다.

    - 여러 객체 책임질 때 문제   
    목적이 같고 코드가 중복되는가? 아니면 코드가 우연히 중복되는가?   

    예를 들어, 함수를 통해 알아보면
    ```Swift
    // 2개의 숫자를 더하는 함수
    func add(_ number1: Int, _ number2: Int) -> Int{
        number1 + number2 = number
    }

    // 숫자를 출력해주는 함수
    func printNumber(_ number: Int) {
        print(number)
    }
    ```
    위 `add(_ number1:, _ number2)` 메서드와 `printNumber(_ number: Int)` 메서드는 단일 책임 원칙을 잘지키고 하나의 역할씩을 가지고 있다.   
    헌데 함수의 수를 줄이기 위해 아래와 같이 합친다면 이 부분은 단일 책임 원칙을 따르지 않는다는 것이다.   
    ```Swift
    func addPrint(_ number1: Int, _ number2: Int) {
        print(number1 + number2)
    }
    ```
    위 예제보다 클래스의 경우를 들어 살펴보자.
    ```Swift
    class Person {
        var age: Int
        var name: String

        func eat() { ... }
        func walk() { ...}
        func speak() { ...}

        func printPersonState() { 
            print("이 사람의 나이는: \(self.age)이고 이름은: \(self.name)이다")
        }
        func logPersonState() { 
            logger.log("현재 나이: \(self.age), 이름: \(self.name)")
        }
    }
    ```
    위와 같이 Person 사람이라는 객체의 `속성`으로는 `나이(age), 이름(name)`와   
    `기능`으로는 `먹기(eat), 걷기(walk), 말하기(speak)` 그리고 `사람의 상태를 출력해주는기능(printPersonState), 사람의 상태를 기록으로 남기는(logPersonState)`의 메서드가 있다.   
    헌데 여기서 사람의 상태를 출력해주는 기능과 사람의 상태를 기록으로 남기는 메서드는 우리가 흔히 아는 사람이 하는 기능과는 동떨어진 얘기다.   
    하여 단일 책임 원칙에 위배되고, 이를 분리하여 작성해 원칙을 따르게하면 아래와 같다.
    ```Swift
    class Person {
        var age: Int
        var name: String

        func eat() { ... }
        func walk() { ...}
        func speak() { ...}

        func represent() -> String {
            return "이 사람의 나이는: \(self.age)이고 이름은: \(self.name)이다"
         }
    }
    let jason = Person()
    print(jason.represent())
    logger.log(jason.represent())
    ```
    위와 같이 사람에 관련된 속성과 기능만 남기고 분리할 수 있는 부분은 분리해주도록 한다.
        
1. 개방-폐쇄 원칙(OCP: Open-Close-Principle)
    
    확장에 열려있고 변경에 닫혀있다.
    
    == 기능을 추가할수는 있어도 기존의 기능을 수정하지 않도록 하자.
    
    (Enum vs Protocol) → Enum은 규칙 위반이지만 Protocol은 원칙에 합당하다.
    
    🤔  그런데 프로토콜은 항상 OCP를 충족시켜줄 수 있을까??
    
    결국.. 정답은 없다… 어떤 방향으로 나아갈 지 모를 수 있지만 예측이 된다면 최대한 지키면서 가야한다.
    
2. 리스코프 치환 원칙(LSP: Liskov Substitution Principle)
    
    자식 클래스는 부모 클래스로써의 역할을 완벽히 할 수 있어야한다.
    
    자신의 속성을 위해 부모 클래스 기능을 거부 / 퇴화
    
3. 의존성 역전 원칙(DIP: Dependency Inversion Principle)
    - 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안된다. → 구체적인 것은 잘 변한다.
    - 구체적인 사항은 추상화에 의존해야한다. → 추상적인건 잘 안변한다.
    - delegate가 가장 대표적인 예
4. 인터페이스 분리 법칙(ISP: Interface Segregation Principle)
    - 클라이언트가 불필요한 자신이 사용하지 않는 인터페이스에 의존하지 말아야한다.
    - 상속받은 메서드를 퇴화시켜야하는 경우가 발생할 수 있음
    - 불필요한 인터페이스에 의존하여 불필요한 빌드가 유발될 수 있음
    - 큰 인터페이스를 작은 인터페이스들로 분리하고,
    필요한 부분만 클라이언트가 취사선택하여 사용할 수 있게 해야함.