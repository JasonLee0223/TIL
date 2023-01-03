# 1️⃣ 단일 책임 원칙(SRP: Single-Responsibility Principle)

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
