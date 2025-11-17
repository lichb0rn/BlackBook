---
up:
  - "[[Golang]]"
related: "[[Observability]]"
created: 2025-05-22
---
Можно экспортировать полезные метрики в [[Golang]]:

```go
expvar.NewString("version").Set(version)
expvar.Publish("database", expvar.Func(func() any {
	return db.Stats()
}))
expvar.Publish("goroutines", expvar.Func(func() any {
	return runtime.NumGoroutine()
}))
```

При этом у `expvar` есть [[Middleware|middleware]], чтобы serve'ить по [[HTTP]]:
```go
r.With(app.BasicAuthMiddleware()).Get("/metrics", expvar.Handler().ServeHTTP)
```