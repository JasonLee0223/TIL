# UIStackView
여러 개의 뷰를 정렬해서 나타낼 때 능률적인 인터페이스이다.   
공식사이트에서 말하길 `열(row) 또는 행(column)에 뷰 컬렉션을 배치하기 위한 간소화된 인터페이스`라고 한다.   
다시 말하면 줄줄이 나열하는 뷰들의 경유 **스택뷰**를 활용하면 간단하게 나타낼 수 있다는 뜻이다.

## StackView를 사용하여 AutoLayout 설정하기
첫 번째로 stackView는 2가지로 나눌 수 있다.   
- 1️⃣ Horizontal(세로 형식)
- 2️⃣ Vertical(가로 형식)
  
가장 큰 특징으로 **StackView 안의 뷰들의 Constraints을 설정하지 않아도 된다.**   
하지만 **스택뷰의 위치 정도는 AutoLayout으로 잡아줘야 사용할 수 있다.**   
스택뷰는 `내부 뷰의 크기에 따라 사이즈(width, height)가 자동`으로 정해지기 때문에 Top, Leading(혹은 Trailing)으로 스택뷰의 `**위치**`만 설정해주어도 AutoLayout이 설정된다.

### Spacing (간격)
View들 간에 간격이 있어야 하는 경우 Spacing을 주면 되는데 `Spacing은 스택뷰 안의 뷰 간 간격을 설정`할 때 사용한다.

### Alignment (조정)
그 외 서로 다른 크기를 가진 View들을 스택뷰를 이용하여 정렬할 때, Aligment를 이용하면 좀 더 세부적인 설정이 가능하다.
- 1️⃣ Horizontal   
  |Fill|Top|Center|Bottom|
  |---|---|---|---|
  |채우기|위쪽 정렬|가운데 정렬|밑쪽 정렬|
  
- 2️⃣ Vertical
  |Fill|Leading|Center|Trailing|
  |---|---|---|---|
  |채우기|왼쪽 정렬|가운데 정렬|오른쪽 정렬|

### Distribution (분배)
**스택뷰 안의 뷰들의 관계**를 나타낼 때 사용하는 것으로 5가지 종류로 정의할 수 있다.
- Fill   
    내가 맞춘 크기에 맞게 뷰들을 채우기 때문에 Priority를 사용자가 직접 설정해줘야한다.
- Fill Equally   
    모든 뷰들의 크기를 `같게` 맞춰준다.
- Equal Spacing   
    뷰들 간의 간격을 동일하게 한다.
- Equal Centering   
    컨첸츠들의 가운데를 기준으로 간격이 맞춰진다.
- Fill Proportionally   
    컨첸츠의 크기가 크면 여백이 커지고, 컨텐츠의 크기가 작으면 여백이 작아진다.

### 🌐 참고사이트   
[UIStackView | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uistackview)   
[iOS) Auto Layout 정복하기 (4/5) - 스택뷰(Stack View)](https://babbab2.tistory.com/154)