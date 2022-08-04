# UIImageView
단일 이미지 또는 일련의 애니메이션 이미지를 인터페이스에 표시하는 개체.
예를 들어, JPEG 또는 PNG 파일과 같은 많은 표준 이미지 파일의 내용을 표시할 수 있다.
애니메이션 이미지의 경우 이 클래스의 메서드를 사용하여 애니메이션을 시작 및 중지하고 다른 애니메이션 매개변수를 지정할 수도 있다.

## 간단한 실습 예시
```Swift
let firstCardImage: UIImageView = {
       let firstCardImage = UIImageView()
        firstCardImage.image = UIImage(named: "c2")
        return firstCardImage
    }()
```
`UIImageView.image`에는 UIImage 객체가 들어갈 수 있고 Asset에 넣어둔 .jpg 또는 여러 형식의 이미지를 불러올 수 있다.

## 이미지 크기 조정 방법 이해
UIImageView에는 이미지 사이즈를 표시하는 방식인 `contentMode`라는 속성이 있고 아래의 프로퍼티를 사용하여 사이즈를 조절할 수 있다.
- scaleAspectFit & scaleAspectFill   
  이미지의 원래 종횡비를 유지하면서 공간에 맞게 이미지 크기를 조정하거나 공간을 채운다.
- scaleToFill   
  원랴 종횡비에 관계없이 이미지의 크기를 조정하므로 **이미지가 왜곡되어 나타날 수 있다.**
- 이 외의 다른 `contentMode`는 크기를 조정하지 않고 ImageView의 경계에서 적절한 위치에 이미지를 배치한다.

### 🌐 참고사이트   
[[UIImageView] Apple-Developer](https://developer.apple.com/documentation/uikit/uiimageview)   
[[Swift]UIImageView 기본 사용법과 CornerRadius와 Shadow넣기](https://tong94.tistory.com/20)   