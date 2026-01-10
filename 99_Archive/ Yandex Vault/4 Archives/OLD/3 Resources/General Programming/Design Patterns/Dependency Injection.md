---
uuid: 20210712152405
created: 2021-07-12T15:24:05
alias:
- dependency injection
- внедрение зависимости
- DI
---

# [[Dependency Injection]]

*Dependency Injection* - паттерн проектирования, при котором зависимости объекту предоставляются "снаружи".

Dependency Injection — мощный механизм отделения конструирования от использования, практическое применение обращения контроля (IoC, [[Inversion of Control]]) в области управления зависимостями. 

Обращение контроля перемещает вторичные обязанности объекта в другие объекты, созданные специально для этой цели, тем самым способствуя соблюдению принципа единой ответственности. В контексте управления зависимостями объект не должен брать на себя ответственность за создание экземпляров зависимостей. Вместо этого он передает эту обязанность другому «уполномоченному» механизму. Так как инициализация является глобальной областью ответственности, этим уполномоченным механизмом обычно является либо функция `main`, либо специализированный контейнер.

## Типы внедрений
- **Initializer**: The consumer provides dependencies to the object-under-construction’s initializer when instantiating the object-under-construction. To enable this, you add dependencies to the object-under-construction’s initializer parameter list. This is the best injection type because the object-under-construction can store the dependency in an immutable stored-property.
- **Property**: After instantiating the object-under-construction, the consumer provides a dependency to the object-under-construction by setting a stored-property on the object-under-construction with the dependency.
- **Method**: The consumer provides dependencies to the object-under-construction when calling a method on the object-under-construction. Method injection is rarely used; however, it’s another option at your disposal. If a dependency is only used within a single method, then you could use method injection to provide the dependency.

### Circular dependencies
Sometimes, two objects are so closely related to each other that they need to depend on one another. For this case to work when using Dependency Injection, you have to use property or method injection in one of the two objects that are in the circular dependency.

## Substituting dependency implementations
Можно выделить два способа замены одних зависимостей другими:
- [[Compile-time substitution]]
- [[Runtime substitution]]

There are several approaches to putting [[Dependency Injection]]:

- **On-demand**: In this approach, you create dependency graphs when needed in a decentralized fashion. This approach is simple yet not very practical. You can use this approach to solidify your understanding of the fundamentals and to feel some of the pain addressed by more advanced approaches.
- **[[Abstract Factory|Factories]]**: Here, you begin to centralize initialization logic. This approach is also fairly simple and is designed to help you learn the fundamentals.
- **Single container**: This approach packages all the initialization logic together into one container. Since there’s state involved, it’s a bit more difficult to put into practice than the previous two approaches.
- **Container hierarchy**: One of the problems with centralizing all the initialization logic is you end up with one massive class. You can break a single container down into a hierarchy of containers. That’s what this approach is all about.

[[A Swift-y Approach to Dependency Injection]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Advanced iOS App Architecture]]
- 🏷️ Tags:: [[Software Design Patterns]],