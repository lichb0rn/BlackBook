---
uuid: 20220720092914
created: 2022-07-20T09:29:14
alias:
---

# [[Async-Await in Javascript]]

## `async` keyword

The `async` keyword is what lets the [[JavaScript]] engine know that you are declaring an asynchronous function. This is required to use `await` inside any function. When a function is declared with `async`, it automatically returns a promise; returning in an `async` function is the same as resolving a promise. Likewise, throwing an error will reject the promise.

An important thing to understand is `async` functions are just syntactical sugar for `promises`.

```javascript
const yourAsyncFunction = async () => {
    // do something asynchronously and return a promise
    return result;
}

anArray.forEach(async item => {
   // do something asynchronously for each item in 'anArray'
   // one could also use .map here to return an array of promises to use with 'Promise.all()'
 });

server.getPeople().then(async people => {
  people.forEach(person => {
    // do something asynchronously for each person
  });
});
```

## `await` keyword
`await` is pretty simple: it tells [[JavaScript]] to wait for an asynchronous action to finish before continuing the function. It’s like a ‘pause until done’ keyword. The `await` keyword is used to get a value from a function where you would normally use `.then()`. Instead of calling `.then()` after the asynchronous function, you would simply assign a variable to the result using `await`. Then you can use the result in your code as you would in your synchronous code.

## Error handling
Handling errors in `async` functions is very easy. Promises have the `.catch()` method for handling rejected promises, and since async functions just return a promise, you can simply call the function, and append a `.catch()` method to the end.

```javascript
asyncFunctionCall().catch(err => {
  console.error(err)
});
```

But there is another way: the mighty `try/catch` block! If you want to handle the error directly inside the `async` function, you can use `try/catch` just like you would inside synchronous code.
```javascript
async function getPersonsInfo(name) {
  try {
    const people = await server.getPeople();
    const person = people.find(person => { return person.name === name });
    return person;
  } catch (error) {
    // Handle the error any way you'd like
  }
}
```


## `async` class methods
```javascript
class Waiter {
  async wait() {
    return await Promise.resolve(1);
  }
}

new Waiter()
  .wait()
  .then(alert); // 1 (this is the same as (result => alert(result)))
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Additional reading:: [javascript.info](https://javascript.info/async-await), [pouchdb](https://pouchdb.com/2015/03/05/taming-the-async-beast-with-es7.html)