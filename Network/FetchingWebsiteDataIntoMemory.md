# Fetching Website Data into Memory

> For small interactions with remote servers, you can use the `URLSessionDataTask` class to receive response data into memory (as opposed to using the `URLSessionDownloadTask` class, which stores the data directly to the file system).   
> A data task is ideal for uses like calling a web service endpoint.

원격 서버와의 작은 상호 작용의 경우 `URLSessionDataTask` 클래스를 사용하여 응답 데이터를 메모리로 수신할 수 있습니다.   
(데이터를 파일 시스템에 직접 저장하는 `URLSessionDownloadTask` 클래스를 사용하는 것과 반대).

> A data task is ideal for uses like calling a web service endpoint.    

데이터 작업은 웹 서비스 endPoint(끝점) 호출과 같은 용도에 이상적이다.

> You use a URL session instance to create the task.    
> If your needs are fairly simple, you can use the shared instance of the URLSession class.

URLSession 인스턴스를 사용하여 Task를 생성합니다.
요구 사항이 매우 단순하다면 URLSession 클래스의 `shared` 인스턴스를 사용할 수 있습니다.

> If you want to interact with the transfer through delegate callbacks,     
> you’ll need to create a session instead of using the shared instance.

`delegate의 콜백(callback)`을 통해 전송과 상호 작용하려면 `shard` 인스턴스를 사용하는 대신 Session(세션)을 만들어야합니다.

> You use a `URLSessionConfiguration` instance when creating a session,   
> also passing in a class that implements `URLSessionDelegate` or one of its subprotocols.

Session(세션)을 생성할 때 `URLSessionConfiguration` 인스턴스를 사용하고 `URLSessionDelegate` 또는 하위 프로토콜 중  
하나를 구현하는 클래스도 전달합니다. (URLSessionDelegate의 하위 프로토콜 중)

> Sessions can be reused to create multiple tasks, so for each unique configuration you need,   
> create a session and store it as a property.

Session(세션)을 재사용하여 여러 작업을 생성할 수 있으므로 필요한 각 unique configuration에 대해 세션을 생성하고 저장 프로퍼티로 저장합니다.

> Once you have a session, you create a data task with one of the dataTask() methods.   
> Tasks are created in a suspended state, and can be started by calling `resume()`.

세션이 있으면 dataTask() 메서드 중 하나를 사용하여 데이터 작업을 만듭니다.  
작업은 일시 중단된 상태에서 생성되며 `resume()`을 호출하여 시작할 수 있습니다.

---
### ⚠️ Note
Be careful to not create more sessions than you need.   
For example, if you have several parts of your app that need a similarly configured session,    
create one session and share it among them.

필요한 것보다 더 많은 세션을 만들지 않도록 주의합니다!  
예를 들어, **`유사하게 구성된 세션이 필요한 앱의 여러 부분이 있는 경우 하나의 세션을 생성하고 공유합니다.`**

---

## Receive Results with a CompletionHandler <br/>(CompletionHandler를 통한 전송 결과 받기)
데이터를 가져오는 가장 간단한 방법은 CompletionHandler를 사용하는 dataTask를 만드는 것입니다.   
이 배열을 통해 작업은 서버의 응답, 데이터 및 가능한 오류를 사용자가 제공하는 CompletionHandler 블록(Block)으로 전달합니다.
<img src = "https://user-images.githubusercontent.com/92699723/224867355-c7f45c80-6e5b-4f42-bb19-fcea98272b3d.png" width=700>

CompletionHandler를 사용하는 dataTask를 생성하려면 URLSession의 `dataTask(with:)` 메서드를 호출합니다.  
CompletionHandler는 아래의 3가지 작업을 수행해야 합니다.

1. 오류 파라미터(매개변수)가 nil인지 확인하십시오.  
그렇지 않으면 전송 오류가 발생한 것입니다. 오류를 처리하고 종료하도록 합니다.

2. 응답(response) 매개변수를 확인하여 상태 코드가 성공을 나타내고 MIME 유형이 예상 값인지 확인합니다.   
그렇지 않은 경우 서버 오류를 처리하고 종료합니다.

3. 필요에 따라 data 인스턴스를 사용합니다.

```Swift
func startLoad() {
    let url = URL(string: "https://www.example.com/")!
    let task = URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            self.handleClientError(error)
            return
        }
        guard let httpResponse = response as? HTTPURLResponse,
            (200...299).contains(httpResponse.statusCode) else {
            self.handleServerError(response)
            return
        }
        if let mimeType = httpResponse.mimeType, mimeType == "text/html",
            let data = data,
            let string = String(data: data, encoding: .utf8) {
            DispatchQueue.main.async {
                self.webView.loadHTMLString(string, baseURL: url)
            }
        }
    }
    task.resume()
}
```
---
### 🔥 Important
> The completion handler is called on a different Grand Central Dispatch queue than the one that created the task.    

CompletionHandler는 Task를 생성한 것과 다른 GCD Queue에서 호출됩니다.   

> Therefore, any work that uses data or error to update the UI — like updating webView — should be explicitly     
> placed on the main queue, as shown here.

따라서 데이터 또는 오류를 사용하여 UI를 업데이트하는 모든 작업(ex. webView 업데이트)은 여기에 표시된 것처럼     
main Queue에 배치되어야합니다.

---

## Receive Transfer Details and Results with a Delegate (Delegate를 통한 전송 세부 정보 및 결과 받기)
> For a greater level of access to the task’s activity as it proceeds, when creating the data task,     
> you can set a delegate on the session, rather than providing a completion handler.

진행 중인 작업 활동에 대한 더 높은 수준의 액세스를 위해 데이터 작업을 생성할 때 CompletionHandler를 제공하는 대신   
Session에서 Delegate를 설정할 수 있습니다.

<img src = "https://user-images.githubusercontent.com/92699723/224868563-4b15d705-f75f-4e6b-841c-dcc977778e25.png" width=700>

> With this approach, portions of the data are provided to the urlSession(_:dataTask:didReceive:) method of URLSessionDataDelegate as they arrive, until the transfer finishes or fails with an error.

이 접근 방식을 사용하면 전송이 완료되거나 오류로 실패할 때까지 데이터의 일부가 URLSessionDataDelegate의     
urlSession(_:dataTask:didReceive:)의 메서드에 도착하면 제공됩니다.

> The delegate also receives other kinds of events as the transfer proceeds.

Delegate는 전송이 진행됨에 따라 다른 종류의 이벤트도 수신합니다.

> You need to create your own URLSession instance when using the delegate approach, rather than     
> using the URLSession class’s simple shared instance.

이 방법은 URLSession 클래스의 단순 shard 인스턴스를 사용하는 대신 Delegate 접근 방식을 사용하기에   
고유한 URLSession 인스턴스를 만들어야합니다.

```Swift
private lazy var session: URLSession = {
    let configuration = URLSessionConfiguration.default
    configuration.waitsForConnectivity = true
    return URLSession(configuration: configuration,
                      delegate: self, delegateQueue: nil)
}()
```

위 코드는 session 인스턴스를 생성하는 방법에 대한 예시입니다.    
아래의 코드는 위 session 인스턴스를 사용하여 데이터 작업을 시작하고 Delegate call back을 사용하여 수신된    
데이터 및 오류를 처리하는 startLoad() 메서드를 보여줍니다.  

```Swift
var receivedData: Data?

func startLoad() {
    loadButton.isEnabled = false
    let url = URL(string: "https://www.example.com/")!
    receivedData = Data()
    let task = session.dataTask(with: url)
    task.resume()
}

// delegate methods

func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didReceive response: URLResponse,
                completionHandler: @escaping (URLSession.ResponseDisposition) -> Void) {
    guard let response = response as? HTTPURLResponse,
        (200...299).contains(response.statusCode),
        let mimeType = response.mimeType,
        mimeType == "text/html" else {
        completionHandler(.cancel)
        return
    }
    completionHandler(.allow)
}

func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didReceive data: Data) {
    self.receivedData?.append(data)
}

func urlSession(_ session: URLSession, task: URLSessionTask, didCompleteWithError error: Error?) {
    DispatchQueue.main.async {
        self.loadButton.isEnabled = true
        if let error = error {
            handleClientError(error)
        } else if let receivedData = self.receivedData,
            let string = String(data: receivedData, encoding: .utf8) {
            self.webView.loadHTMLString(string, baseURL: task.currentRequest?.url)
        }
    }
}
```
