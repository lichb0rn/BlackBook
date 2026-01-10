---
uuid: 20220802160147
created: 2022-08-02T16:01:47
alias: общепринятые соглашения в Node.js
---

# [[Node.js callback conventions]]

## The callback comes last
In all core Node.js functions, the standard convention is that when a function accepts a callback as input, this has to be passed as the last argument.
`readFile(filename, [options], callback)`

## Any error always comes first
In [[Continous Propagation Style|CPS]], errors are propagated like any other type of result, which means using callbacks. In Node.js, any error produced by a CPS function is always passed as the first argument of the callback, and any actual result is passed starting from the second argument. If the operation succeeds without errors, the first argument will be `null` or `undefined`. 
```javascript
readFile('foo.txt', 'utf8', (err, data) => {
	if(err) {
		handleError(err)
	} else {
		processData(data)
	}
})
```

It is best practice to **always check for the presence of an error,** as not doing so will make it harder for you to debug your code and discover the possible points of failure. Another important convention to take into account is that **the error must always be of type Error**. This means that simple strings or numbers should never be passed as error objects.

## Propagating errors
Propagating errors in synchronous, direct style functions is done with the well-known throw statement, which causes the error to jump up in the call stack until it is caught.

In asynchronous CPS, however, proper error propagation is done by simply passing
the error to the next callback in the chain. 

```javascript
import { readFile } from 'fs'
function readJSON (filename, callback) {
	readFile(filename, 'utf8', (err, data) => {
		let parsed
		if (err) {
			// propagate the error and exit the current function
			return callback(err)
		}
		try {
			// parse the file contents
			parsed = JSON.parse(data)
		} catch (err) {
			// catch parsing errors
			return callback(err)
		}
		// no errors, propagate just the data
		callback(null, parsed)
	})
}
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note