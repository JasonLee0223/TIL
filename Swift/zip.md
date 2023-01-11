# zip
Create a sequence of pairs built out of two underlying sequences.
2가지의 기본 Sequence(연속성을 가진 타입 ex. 배열)를 한 쌍의 Sequence로 사용하도록 해줍니다.

## Declaration
```Swift
func zip<Sequence1, Sequence2>(
    _ sequence1: Sequence1,
    _ sequence2: Sequence2
) -> Zip2Sequence<Sequence1, Sequence2> where Sequence1 : Sequence, Sequence2 : Sequence
```

## Example
```Swift
let words = ["one", "two", "three", "four"]
let numbers = 1...4

for (word, number) in zip(words, numbers) {
    print("\(word): \(number)")
}
// Prints "one: 1"
// Prints "two: 2
// Prints "three: 3"
// Prints "four: 4"
```

## Practice
```Swift
func currentStockDisplay(on emojiLabels: [UILabel], change countLabels: [UILabel]) {
    for (emojiLabel, countLabel) in zip(emojiLabels, countLabels) {
        guard let checkTest = emojiLabel.text else {
            return
        }
        
        switch checkTest {
        case "🍓":
            countLabel.text = currentStock(fruitName: .strawberry)
        case "🍌":
            countLabel.text = currentStock(fruitName: .banana)
        case "🍍":
            countLabel.text = currentStock(fruitName: .pineApple)
        case "🥝":
            countLabel.text = currentStock(fruitName: .kiwi)
        case "🥭":
            countLabel.text = currentStock(fruitName: .mango)
        default:
            return
        }
    }
}
```