# 13. HTTP Middleware ([Golang Backend Training](../../README.md))

## 13.1. What is HTTP Middleware

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


**Make Go HTTP middleware that takes an `http.Request`**, if it does NOT have an `X-HTTP-Method-Override` HTTP request header, then it just passes that `http.Request` to the sub- `http.Handler`, but if it does indeed have an `X-HTTP-Method-Override` HTTP request header

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

## 13.2. X-HTTP-Method-Override

HTTP was designed such that _HTTP paths_ (such as `http://example.com/members/joe-blow`) represents _nouns_, and _HTTP methods_ (such as built-in ones such as `DELETE`, `GET`, `PATCH`, `POST`, `PUT`, and custom ones such as `KICK`, `PUNCH`, `SCREAM`, etc) represent _verbs_.

(Because many people were unaware that this was part of the original HTTP design and how HTTP was intended to be used, some came up with a new name for this — “REST”. But this was just how HTTP was intended to be used.)

Some HTTP client software cannot use _all_ the built-in HTTP methods (such as `DELETE`, `GET`, `PATCH`, `POST`, `PUT`), and cannot use custom HTTP methods (such as `KICK`, `PUNCH`, `SCREAM`, etc).

Some HTTP client software is unfortunately limited to just `GET` & `POST`.

Due to this, a work-around was created: `X-HTTP-Method-Override`

Here is an HTTP request of the `X-HTTP-Method-Override` HTTP request header being used:

```
POST /members/joe-blow HTTP/1.1
Host: example.com
X-HTTP-Method-Override: PATCH
Content-Type: application/x-www-form-urlencoded
Content-Length: 25

phone_number=604-555-5555
```

The `X-HTTP-Method-Override` work-around works like this:

If you do an HTTP `POST` on a URL, and include the `X-HTTP-Method-Override` HTTP request header, then it is as if you did this:

```
PATCH /members/joe-blow HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 25

phone_number=604-555-5555

```

(Notice in this second HTTP request code that the `X-HTTP-Method-Override` HTTP request header is gone, and the `POST` at the beginning is replaced by `PATCH`.)

## 13.3. X-HTTP-Method-Override HTTP Middleware

Create Go HTTP Middleware that does handles the `X-HTTP-Method-Override` HTTP request header.

So, something like:

```go
type XHTTPMethodOverrideHandler struct {
	SubHandler http.Handler
}

func (receiver XHTTPMethodOverrideHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	//@TODO
}
```

With this, the HTTP request is represented by `http.Request` you need to check to if the `X-HTTP-Method-Override` HTTP request header is there or not.

If it is NOT there, then you can pass the `http.Request` to the sub-`http.Handler` as is.

But it is in there, you either need to modify `http.Request` (changing the HTTP method, and removeing the `X-HTTP-Method-Override` HTTP request header) before passing it, or create a new one to pass.

**And of course create a program that uses this, to make sure it works.**

**And, as always, create units tests for your new `XHTTPMethodOverrideHandler` type.**

Hints:
* [http.Handler](https://pkg.go.dev/net/http#Handler)
* [http.Request](https://pkg.go.dev/net/http#Request)

## 13.4. User-Agent Logging HTTP Middleware

Create Go HTTP Middleware that logs the User-Agent for an HTTP request.

Hints:
* [http.Handler](https://pkg.go.dev/net/http#Handler)
* [http.Request](https://pkg.go.dev/net/http#Request)
* [User-Agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent)

-----

[⏮](../golang-project-structure/README.md) [⏭️](../http_router/README.md)
