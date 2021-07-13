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
	subhandler.ServerHTTP(w, r) // <----
	log.End()
}
```

(Note that I've tried to keep things simpler in this `ServeHTTP()` to make it easier to understand. A production ready `ServeHTTP()` method would have more.)

**Pay close attention to what is happening.**

The `LogHandler`we created is has its own `ServeHTTP()` method that calls another `http.Handler`'s `ServeHTTP()` method.

The `LogHandler` does some stuff before and after calling the other `http.Handler's` `ServeHTTP()` method. In this case, it is logging. But conceptually we could make it do whatever we want.

This is what many call **“HTTP middleware”**. (Although many also just shorten that to **“middleware”**.)

So, how would we use this‽ — here is how:

This is what your code might look with **WITHOUT** the `LogHandler`:
```go
// main.go
package main

import (
	"srv/log"

	"fmt"
	"net/http"
)

const (
	httpAddr = ":8080"
)

type helloWorldHandler struct{}

func (receiver helloWorldHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello world!")
}

func main() {
	log := logsrv.Begin()
	defer log.End()

	log.Inform("HTTP Address:", httpAddr)

	var handler http.Handler // <---
	
	handler = helloWorldHandler{} // <----

	err := http.ListenAndServe(httpAddr, handler) // <----
	if nil != err (
		log.Error("Had problem with HTTP server:", err)
		return
	}
}
```

And this is what your code might look with **WITHOUT** the `LogHandler`:
```go
// main.go
package main

import (
	"srv/log"

	"fmt"
	"net/http"
)

const (
	httpAddr = ":8080"
)

type helloWorldHandler struct{}

func (receiver helloWorldHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello world!")
}

func main() {
	log := logsrv.Begin()
	defer log.End()

	log.Inform("HTTP Address:", httpAddr)

	var handler http.Handler // <---
	
	handler = helloWorldHandler{} // <----
	
	handler = LogHandler{
		SubHandler: handler, // <---- WE ARE WRAPPING THE PREVIOUS HANDLER
	}

	err := http.ListenAndServe(httpAddr, handler) // <----
	if nil != err (
		log.Error("Had problem with HTTP server:", err)
		return
	}
}
```
