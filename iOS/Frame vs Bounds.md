# Frame vs Bounds
- Geometry: 뷰에 대한 위치와 크기
Superview's coordinate Space

- Frame & Center: 좌표 공간을 따라간다.

- Bounds: View's coordinate Space / 자기 자신의 크기를 의미, 내 좌표 시스템

- CGRect는 `View의 위치(origin)와 크기(size)`를 나타내기 위해 사용되고   
frame & bounds는 View의 위치와 크기를 보여주게된다.

- 🟡 frame과 bounds의 `size(width, height)는 동일`하지만,   
  `origin(x, y)값이 다르다.`

## Frame
`SuperView 좌표계`에서 View의 위치와 크기를 나타낸다.

### SuperView란?
View의 계층 구조에서 내 View의 `한 칸 윗 계층 View`를 말한다.
Ex) secondView의 SuperView는 firstView가 된다.  
(FirstView의 SuperView는 RootView)  
<img src="https://user-images.githubusercontent.com/92699723/190225906-fabc712a-813e-4498-9fc0-bac0c00e5457.png" width="200" height="200">  

### Frame의 origin(x, y)
SuperView의 원점이 (0, 0)을 기준으로 `원점으로부터 얼마나 떨어져 있는지`를 나타내는 것.

### Frame의 size(width, height)
`View 영역을 모두 감싸는 사각형`으로 나타낸 것.   
frame의 size는 View 자체의 크기가 아니라 `View가 차지하는 영역을 감싸서 만든 사각형`을 frame의 size라고 본다.   

## Bounds
`자신의 좌표계`에서 View의 위치와 크기를 나타낸다.
frame이 SuperView의 좌표계였다면, bounds는 자신의 좌표계
(위에 영문으로 설명한 내용을 다시보면 superview vs view의 차이)   

### Bounds의 origin(x, y)
frame과 달리 Superview와는 아무 상관이 없으며 오로지 `자기 자신(view)을 기준`으로한다. = 자신의 원점을 (0, 0)으로 놓는다.
즉, 좌표의 시작점을 자기의 원점으로 놓는다.

### Bounds의 size(width, height)
`View 자체의 영역`을 나타낸 것.
bounds는 View 자체의 영역을 나타내기 때문에   
frame처럼 View 영역을 모두 감싼 사각형이 아니다.

## 결론
| |frame|bounds|
|---|---|---|   
|origin(x, y)| SuperView Coordinate| View Coordinate|
|size(width, height)|View 영역을 모두 감싸는 사각형| View 영역 자체|

### 참고사이트 🌐
[iOS) Frame vs Bounds 제대로 이해하기 (1/3)](https://babbab2.tistory.com/44)   
[iOS) Frame vs. Bounds](https://sihyungyou.github.io/iOS-frame-bounds/)   
[Apple Developer Documentation - Frame](https://developer.apple.com/documentation/uikit/uiview/1622621-frame)   
[Apple Developer Documentation - Bounds](https://developer.apple.com/documentation/uikit/uiview/1622580-bounds) 

