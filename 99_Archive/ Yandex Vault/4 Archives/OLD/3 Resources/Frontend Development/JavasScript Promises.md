---
uuid: 20220717100555
created: 2022-07-17T10:05:55
aliases:
  - Promises
  - промис
---

# [[JavasScript Promises]]

`Promise`  в [[JavaScript]] используется для отложенных и асинхронных операций.

## Basics
Создаём Promise
```javascript
let p = new Promise(function(resolve, reject) {
	if (/* good */) {
		resolve('Success');
	} else {
		reject('Bad');
	}
});

p.then(function(result) {
	/* do smth with result */
}).catch(function() {
	/* error */
}).finally(function() {
	/* executes regardless of success or failuer */
})
```

>[!Note] 
>Как только `Promise` исполняется, он становится **immutable**.


## Promise.all
`Promise.all` принимает массив из промисов и выполняется, когда все они исполнятся.
```javascript
Promise.all([promise1, promise2]).then(function(results) {
	// Both promises resolved
})
.catch(function(error) {
	// One or more promises was rejected
});
```

## Promise.race
`Promise.race` похожа на `Promise.all`, но ждёт только одного какого-нибудь промиса
```javascript
var req1 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { resolve('First!'); }, 8000);
});
var req2 = new Promise(function(resolve, reject) { 
	// A mock async action using setTimeout
	setTimeout(function() { resolve('Second!'); }, 3000);
});
Promise.race([req1, req2]).then(function(one) {
	console.log('Then: ', one);
}).catch(function(one, two) {
	console.log('Catch: ', one);
});

// From the console:
// Then: Second!
```

## Промисы и очередь микрозадач
**When a promise is settled, any functions that were waiting for its result are added to a queue called the [[JavaScript Queues|microtask queue]]**. The microtask queue is used to store all of the functions that need to be executed after the current synchronous code has finished running. This means that any functions added to the microtask queue will be executed **before the next block of synchronous code** is run.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note