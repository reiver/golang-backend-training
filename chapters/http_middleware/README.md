# 12. HTTP Middleware ([Golang Backend Training](../../README.md))

# 12.1. What is HTTP Middleware

One of the key components of Go's built-in ["net/http"](https://pkg.go.dev/net/http) package is the [http.Handler](https://pkg.go.dev/net/http#Handler) interface:
```go
type Handler interface {
	ServeHTTP(http.ResponseWriter, *http.Request)
}
```

One powerful trick is to have one `http.Handler` wrap another `http.Handler`

Here is an example:
```go
type LogHandler struct {
	SubHandler http.Handler
}

func (receiver LogHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	subhandler := receiver.SubHandler
	if nil == subhandler {
		http.Error(w, "Internal Server Error", http.StatusInternalServerError)
		return
	}

	log := logsrv.Begin()
	subhandler.ServerHTTP(w, r)
	log.End()
}
```

**Pay close attention to what is happening.**

The `LogHandler`we created is has its own `ServeHTTP()` method that calls another `http.Handler`'s `ServeHTTP()` method.

The `LogHandler` does some stuff before and after calling the other `http.Handler's` `ServeHTTP()` method. In this case, it is logging. But conceptually it could do whatever it wants.

This is what many call **“HTTP middleware”**. (Although many also just shorten that to **“middleware”**.)

So, how would we use this‽ — here is how:
