---
uuid: 20220809090641
created: 2022-08-09T09:06:41
alias: цепочка вызовов в javascript
---

# [[Method chaining in Javascript]]

Make sure to return the current [[JavaScript Object|object]] at the end of each method that should support method chaining. In a custom class, this is usually as simple as adding a `return this` statement.

```javascript
class Book {
  constructor(title, author, price, publishedDate) {
    this.title = title;
    this.author = author;
    this.price = price;
    this.publishedDate = publishedDate;
  }

  raisePrice(percent) {
    const increase = this.price*percent;
    this.price += Math.round(increase)/100;
    return this;
  }

  releaseNewEdition() {
    // Set the pulishedDate to today
    this.publishedDate = new Date();
    return this;
  }
}

const book = new Book('I Love Mathematics', 'Adam Up', 15.99,
 new Date(2010, 2, 2));

// Raise the price 15% and then change the edition, using method chaining
console.log(book.raisePrice(15).releaseNewEdition());
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[JavaScript Cookbook]]