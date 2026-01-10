---
uuid: 20221207172614
created: 2022-12-07T17:26:14
alias: combine subscription lifecycle
---

# [[Subscription Lifecycle]]
![[Pasted image 20221207172703.png]]

1. [[Combine Subscriber]] подписывается на  [[Combine Publisher]]
2. Publisher создаёт [[Combine Subscription]] и передаёт её subscriber'у через `receive(subscription:))`
3. Subscriber запрашивает данные через подписку, отправляя количество значений, которое ему нужно (`request(_:)`)
4. Subscription начинает работу и отдаёт данные. Она отправляет их по одному через метод subscriber `receive(_:)`
5. После получения данных, subscriber возвращает новое значение `Subscibers.Demand`, которое добавляется к прошлому запросу
6. Subscription продолжает отправлять данные, пока не достигнет деманда.

- Если Subscription отправила запрошенное количество данных, она должна ждать нового запроса с новым значением demand.
- Если произошла ошибки или источник данных закончился, то она Subscription вызывает у Subscriber метод `receive(completion:)`.


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Combine Asynchronous Programming with Swift|Combine: Asynchronous Programming with Swift]]
-  🏷️ Tags:: [[Combine]] [[Asynchronous Programming]]