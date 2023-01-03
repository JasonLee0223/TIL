# 2️⃣ 개방-폐쇄 원칙(OCP: Open-Close-Principle)

`확장(Extension)에 열려`있고 `수정(modification)에 닫혀`있다.   
👉🏻 코드에 대한 원칙이 아니라 코드의 행동?에 대한 얘기라 잘와닫지 않는다.   
👉🏻 기능을 추가할수는 있어도 기존의 기능을 수정하지 않도록 하자.

규칙에 위반되는 예시를 들어보자.
```Swift
// OCP 위반 사례
class Cat {
    func makeSound() {
        print("Meow")
    }
}

class Dog {
    func makeSound() {
        print("Bark")
    }
}

class Zoo {
    var dogs: [Dog] = [Dog(), Dog(), Dog()]
    var cats: [Cat] = [Cat(), Cat(), Cat()]

    func makeAllSounds() {
        dogs.forEach { $0.makeSound() }
        cats.forEach { $0.makeSound() }
    }
}
```
위와 같은 코드가 있다고 하였을 때 `Cow(소), Sheep(양)` 이라는 동물이 추가된다고하면   
Zoo 객체의 범주 안에는 `Cat(고양이), Dog(강아지)`만 있는데 이를 소와 양에 대해서 `확장(Extension)`을 하려고 하니   
makeAllSound 메서드를 수정해야하는 상황이 발생하게된다. 당연히 이 부분에서 제한이 생기며 원칙에 위배되게된다.   

이를 개선해보면...!!   
이번에는 `확장(extension)에 대해 열려(Open)`있어서 다른 어떤 동물이 들어와도 자유롭게 확장이 가능하고   
`수정(modification)에 대해서는 닫혀(Close)`있어 메서드를 수정하지 않아도되도록 작성해보자!
```Swift
// OCP에 적합한 코드
protocol Animal {
    func makeSound()
}

class Cat: Animal {
    func makeSound() {
        print("Meow")
    }
}

class Dog: Animal {
    func makeSound() {
        print("Bark")
    }
}

class Zoo {
    var animals: [Animal] = []

    func makeAllSounds() {
        animals.forEach { $0.makeSound() }
    }
}
```
이렇게 Protocol을 활용하여 설계를 진행하면 새롭게 어떤 동물이 추가되어도 `기존의 코드를 변경하지 않고`   
그저 `class 새로운 동물: Animal`로 선언하여 구현하면 해결이 된다.   
이렇게 되면 확장에는 열려있고 수정에는 닫혀있게 된다!!

(Enum vs Protocol) → Enum은 규칙 위반이지만 Protocol은 원칙에 합당하다.

🤔  그런데 프로토콜은 항상 OCP를 충족시켜줄 수 있을까??   
결국.. 정답은 없다… 어떤 방향으로 나아갈 지 모를 수 있지만 예측이 된다면 최대한 지키면서 가야한다.
