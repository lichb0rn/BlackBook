---
uuid: 20221004154948
created: 2022-10-04T15:49:48
alias:
- complext switch
- сложный switch
- switch refactoring
- рефакторинг switch
---

# [[Ветвление switch]]

Пример, пусть у нас есть функция с операцией, зависищей от типа работника:
```java
public Money calculatePay(Employee e) throws InvalidEmployeeType {
	switch (e.type) {
	case COMMISSIONED:
		return calculateCommissionedPay(e);
	case HOURLY:
		return calculateHourlyPay(e);
	case SALARIED:
		return calculateSalariedPay(e);
	default:
		throw new InvalidEmployeeType(e.type);
	}
}
```

Эта функция имеет ряд недостатков. 
- Во-первых, **она велика**, а при добавлении новых типов работников она будет разрастаться. 
- Во-вторых, она совершенно очевидно **выполняет более одной операции**. 
- В-третьих, она **нарушает [[SOLID|принцип единой ответственности]]**, так как у нее существует несколько возможных причин изменения. 
- В-четвертых, она **нарушает [[SOLID|принцип открытости/закрытости]]**, потому что код функции должен изменяться при каждом добавлении новых типов.

Но, пожалуй, самый серьезный недостаток заключается в том, что программа может содержать неограниченное количество других функций с аналогичной структурой, например:
- `isPayday(Employee e, Date date)` 
 или 
- `deliverPay(Employee e, Money pay)` , и так далее. 

Все эти функции будут иметь все ту же ущербную структуру.

Решение проблемы заключается в том, чтобы похоронить команду switch в фундаменте [[Abstract Factory|АБСТРАКТНОЙ ФАБРИКИ]]. 

Фабрика использует команду `switch` для создания соответствующих экземпляров потомков `Employee`, а вызовы функций `calculatePay`, `isPayDay`, `deliverPay` и т.д. проходят полиморфную передачу через интерфейс `Employee`.

```java
public abstract class Employee {
    public abstract boolean isPayday();
    public abstract Money calculatePay();
    public abstract void deliverPay(Money pay);
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}

public class EmployeeFactoryImpl implements EmployeeFactory {
    
    public Employee makeEmployee(EmployeeRecord r) 
	    throws InvalidEmployeeType {
        switch (r.type) {
            case COMMISSIONED:
                return new CommissionedEmployee(r) ;
            case HOURLY:
                return new HourlyEmployee(r);
            case SALARIED:
                return new SalariedEmploye(r);
            default:
                throw new InvalidEmployeeType(r.type);
        }
    }
}
```

---

## 📇 Additional Metadata
- 🛠️ Status:: #📚 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Clean Code A Handbook of Agile Software Craftsmanship]]
- 🏷️ Tags:: [[Software Design Patterns]]