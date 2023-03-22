# CompletionHandler

CompletionHandler는 결국 클로저이다.    
URLSession이나 어떠한 메서드의 완료되는 시점을 파악하고 사용하기 위해서 자주 접하게 되었다.     
예시를 통해 알아보자!   

## 1️⃣ CompletionHandler에 매개변수가 없는 경우
```Swift
// 호출부
// Case 1
temp {
	//...
}

// Case 2
temp(completion: myCompletion)

func myCompletion() {
	//...
}

// 구현부
func temp(completion: @escaping () -> Void) {
	completion()
}
```

## 2️⃣ CompletionHandler에 매개변수가 하나 있는 경우
```Swift
// 호출부
// Case 1
temp { string in
    //...
}

// Case 2
temp(completion: myCompletion)

func myCompletion(myString: String) { }

// 구현부
func temp(completion: @escaping (String) -> ()) {
    completion("String 값을 넣어야합니다!")
}
```

여기까지 보았으면 구현부에서는 `completion`이라는 매개변수를 `스코프({})`안에서 그저 값을 넣어주기만 한다!!   
이 부분이 왜이렇게 어렵게 느껴졌는지...     
```Swift
completion(string값을 넣어주면 된다.)
```

그러면 호출부에서는 completion이 넘겨준 String 값을 통해서 안에서 무언가를 더 구현할 수 있게 된다.  
좀 더 프로젝트에서 사용해보았던 방법을 예시로 보자.

```Swift
var action: UIAction {
    let action = UIAction { [self] _ in
        guard let customers = mainViewdelegate?.sendCustomersInfo() else {
            return
        }
        
        mainViewdelegate?.makeCustomerLabel(customers: customers, completion: { [self] waitingCustomer in

            mainViewdelegate?.drawinigWorkingLabel(of: waitingCustomer, completion: {
                
                // Do Something 
            })
        })
    }
    return action
}
```

```Swift
func makeCustomerLabel(customers: [Customer],
                        completion: @escaping (Customer) -> Void) {
    customers.forEach { currentCustomer in
        let customerInfoLabel : UILabel = {
            let customerInfoLabel = UILabel()
            customerInfoLabel.text = "\(currentCustomer.waitingNumber) - \(currentCustomer.workType)"
            customerInfoLabel.textAlignment = .center
            customerInfoLabel.font = .systemFont(ofSize: 20, weight: .regular)
            
            if currentCustomer.workType == WorkType.loan {
                customerInfoLabel.textColor = .systemPurple
            }
            
            completion(currentCustomer)
            
            return customerInfoLabel
        }()
        
        DispatchQueue.main.async {
            self.subView.waitingStackView.addArrangedSubview(customerInfoLabel)
        }
    }
}
    
func drawinigWorkingLabel(of customer: Customer,
                            completion: @escaping () -> Void) {
    let workingCustomer: UILabel = {
        let workingCustomer = UILabel()
        workingCustomer.text = "\(customer.waitingNumber) - \(customer.workType)"
        workingCustomer.textAlignment = .center
        workingCustomer.font = .systemFont(ofSize: 20, weight: .regular)
        
        return workingCustomer
    }()
    completion()
    
    DispatchQueue.main.async {
        self.subView.workingStackView.addArrangedSubview(workingCustomer)
    }
}
```