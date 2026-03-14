---
tags:
  - type/note
domain: "[[Разработка web-приложений на Go|Go web development]]"
topics:
sources:
---
# Panic recovery in background goroutines

It’s important to realize that our middleware will only recover panics that happen in the same goroutine that executed the `recoverPanic()` middleware.

If, for example, you have a handler which spins up another goroutine (e.g. to do some background processing), then any panics that happen in the second goroutine will not be recovered — not by the `recoverPanic()` middleware… and not by the panic recovery built into [[Golang|Go]] HTTP server. They will cause your application to exit and bring down the server.

So, if you are spinning up additional goroutines from within your web application and there is any chance of a panic, you must make sure that you recover any panics from within those too. For example:


```go
func (app *application) myHandler(w http.ResponseWriter, r *http.Request) {
	...
	// Spin up a new goroutine to do some background processing.
	go func() {
		defer func() {
			if err := recover(); err != nil {
				app.logger.Error(fmt.Sprint(err))
			}
		}()
		doSomeBackgroundProcessing()
	}()
	
	w.Write([]byte("OK"))
}
```