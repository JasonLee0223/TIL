# How to hide my APIKEY

open API를 사용할 때 보통 회원가입을 하여 사용할 수 있게 되는데     
GitHub에서 Tracking을 하지 않도록 하는 방법과 프로젝트 내에서도 안전하게 숨겨서 사용해보고자한다.

우선 PropertyList 파일을 하나 생성한다. (Info.plist와 같은 파일 형식이다.)      
<img src="https://user-images.githubusercontent.com/92699723/224987903-9503f762-7522-4c09-8031-91178b54c904.png">

여기서 `.plist`가 `P`(roperty)`list`의 줄임말이였다는 사실을 처음 알았다..      
아래의 이미지처럼 plist 파일이 생성되고 `API_Key`라는 이름과 Value를 적어준다.
<img src = "https://user-images.githubusercontent.com/92699723/224991367-b410e274-92b1-4293-8012-7caa9eff28e1.png" width=800>

위 이미지에서 Value에 문장으로 적었지만 API Key Value를 넣어주면된다.

저렇게만 넣고나서는 프로퍼티로 사용할 수 없기 때문에 `Bundle`에 넣어서 사용할 수 있도록 Extension을 사용해서 처리한다.
```Swift
extension Bundle {
    var APIKey: String {
        guard let file = self.path(forResource: "API+KEY", ofType: "plist") else {
            return ""
        }
        
        guard let resource = NSDictionary(contentsOfFile: file) else {
            return ""
        }
        
        guard let key = resource["API_Key"] as? String else {
            fatalError("API+KEY에 APIKey를 설정하세요.")
        }
        return key
    }
}
```
Bundle에 넣는 이유는 실행 가능한 코드와 그 코드의 자원을 포함하고 있는 디렉토리이기 때문입니다.
여기까지는 APIKEY를 사용하는 방법이였다.

### 이제 Git이 추적하지 않도록하자!
```
git update-index --skip-worktree 자신의프로젝트명/API+KEY.plist

// Example
git update-index --skip-worktree WeatherForecast/WeatherForecast/Configuration/API+Key.plist
```
