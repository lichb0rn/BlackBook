---
aliases: ["async/await"]
---
MOC:  [[Swift]]

---

Новый синтаксис состоит из трёх сущностей:

- `async`: объявляет, что данная функция будет выполняться асинхронно. 
- `await`: объявляет, что код может встать на паузу, ожидая `async`-функцию
- `Task`: единица асинхронной работы.

Пример кода:
```swift
class API {
  ...
  func fetchServerStatus() async throws -> ServerStatus {
    let (data, _) = try await URLSession.shared.data(
      from: URL(string: "http://amazingserver.com/status")!
    )
    return ServerStatus(data: data)
  }
}

class ViewController {
  let api = API()
  let viewModel = ViewModel()

  func viewDidAppear() {
    Task {
      viewModel.serverStatus = try await api.fetchServerStatus()
    }
  }
}
```

Swift делит код на участки, называемые *partial tasks* или *partials*:
![[Pasted image 20220422092302.png]]

Эти участки выполняются асинхронно и не обязательно на одном потоке. 

Когда код "засыпает" при вызове `await`, Swift создает специальный объект [[Swift Continuation|continuation]], который содержит состояние на момент останова. Когда приходит момент возобновить работу или бросить исключение, система восстанавливает состояние из continuation.