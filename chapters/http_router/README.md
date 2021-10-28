# 14. HTTP Router ([Golang Backend Training](../../README.md))

In this chapter you are going to create an **HTTP router**.

But we will need to work up to it. So there will be a number of steps before we get there.

## 14.1. http.ListenAndServe()

Take a look at this code:
```go
err := http.ListenAndServe(httpAddr, theHandlerYouCreated)
```
(Where `httpAddr` might be something like `":8080"`, and `theHandlerYouCreated` is some type that has a `.ServeHTTP(http.ResponseWriter, *http.Request)` method, so that it matches the `http.Handler` interface.)

When your Go program is a web server, it usually has code like that somewhere.

If you are creating a backend HTTP(S) based API, then your program is a web server.

Recall that in Go, the built-in `"net/http"` package, does most the low-level HTTP work for you.
**But that (in the case of that example code) your `theHandlerYouCreated.ServeHTTP()` method _is_ the web server, in a lot of ways.**

What does that mean —

The `http.ListenAndServe()` function (from Go's built-in `"net/http"` package) will call your `theHandlerYouCreated.ServeHTTP()` method for **all** HTTP requests. All of them!
Doesn't matter the **HTTP path** is. Doesn't matter what the **HTTP method** is. All HTTP requests will be handed off to your `theHandlerYouCreated.ServeHTTP()` method!

If you come from a background of doing web development using an interpretted programming language, such as PHP or Ruby, etc, then this is probably different than how you are used to working.

You are probably used to:

№1: code in different files handling different HTTP requests, and

№2: the path of the that code on the server relating to what HTTP path it is called for.

For example, in PHP you might have the following PHP code:

* /home/username/api.php
  * /home/username/api/v1.php
    * /home/username/api/v1/accounts.php
    * /home/username/api/v1/toys.php
    * /home/username/api/v1/users.php

And then this might get mapped he following way to the code on disk.

* `GET /api` -> `/home/username/api.php`
* `GET /api/v1` -> `/home/username/api/v1.php`
* `GET /api/v1/accounts` -> `/home/username/api/v1/accounts.php`
* `GET /api/v1/toys` -> `/home/username/api/v1/toys.php` 
* `GET /api/v1/users` -> `/home/username/api/v1/users.php`

Go's `http.ListenAndServe()` function doesn't (by default) work this way.
**But you are going to create something to make it work this way.**

But you are going to do it in multiple steps.
First creating a simple **HTTP router**.
And then adding more and more sophistication to it, until you have something powerful.

## 14.2 ServeHTTP Switch Part 1

The first thing you are going to do is create a new type:
```go
type HTTPSwitch struct {
	//@TODO
}
```

This will be an `http.Handler`, so you will need a `.ServeHTTP()` method:
```go
func (receiver *HTTPSwitch) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	//@TODO
}
```

Now what you are going to do is that you will make it look at the **HTTP path** in the **HTTP request** and return something different depending on what the **HTTP path** is. 

The `.ServeHTTP()` method's 2nd parameter is a pointer to an `http.Request`. And `http.Request` tells you (among other things) what the **HTTP path** is. See:

* [http.Request](https://pkg.go.dev/net/http#Request)
* [ur.URL](https://pkg.go.dev/net/url#URL)

Inside of this `.ServeHTTP()` method, use Go's `switch`-stament to return different responses depending on what the **HTTP path** is. For example:
```go

var path = ??? // <--- you have to figure out how to get the HTTP path.

switch path {
case "/hello":
	fmt.Fprint(w, "Hello world!")
	return
case "/favorite/fruits":
	fmt.Fprint(w, "apple banana cherry")
	return
default:
	http.Error(w, "Not FOund", http.StatusNotFound)
	return
}
return
```

Notice that I've made this return something for two paths — `/hello` and `/favorite/fruits"`.
And for everything else it return a **404 Not Found** HTTP response.

**Make this handle 3 other paths.**
You decide what those paths are.
And you decide what it returns for those paths.

Once you have completed this, write a program to test this out, and make sure it works.

## 14.3 ServeHTTP Switch Part 2

Now make it so `/hello` tells you what **HTTP method** was used to request it. For example, change this:
```go
	fmt.Fprint(w, "Hello world!")
```
to this:
```go
	var method = ??? // <--- you have to figure out how to get the HTTP method.

	fmt.Fprintf(w, "Hello world! method = %q", method)
```

The `http.Request` tells you what the **HTTP method** is. See:

* [http.Request](https://pkg.go.dev/net/http#Request)

Once you finish that, use the program you wrote to make sure it works.

## 14.4. HTTP Router with Paths

The **HTTP switch** we created is OK, but it is limited in some ways. Every time we want to add support for a new **HTTP path** we have to edit the `.ServeHTTP()` method.

This is not ideal for many reasons. (One being a high degree of _coupling_.)

What we want is a way of making our type support new **HTTP paths** without having to edit the code for the `.ServeHTTP()` method.

So, you are going to create a new type:
```go
package httprouter

type Router struct {
	//@TODO
}
```

And just like the `HTTPSwitch` you created before, this too will be an `http.Handler`, so it will have a `.ServeHTTP()` method:
```go
func (receiver Router) ServeHTTP(http.ResponseWriter, *http.Request) {
	//@TODO
}
```

But, to make this so you can make it support **HTTP paths** on the fly, you are also going to give this new type this method:
```go
func (receiver Router) Register(handler http.Handler, path string) error {
	//@TODO
}
```

So that you can do things such as:
```go
var router httprouter.Router

// ...

err := httprouter.Register(handleHello, "/hello")

err := httprouter.Register(handleFavoriteFruit, "/favorite/fruits")
```

So, to summarize, your `httprouter.Router` will fit this interface:
```go
interface {
	ServeHTTP(w ResponseWriter, r *Request)
	Register(handler http.Handler, path string) error
}
```

Once you finish that, use the program you wrote to make sure it works.

## 14.5. HTTP Router with Paths and Methods

Now lets change the `.Register()` method from this:
```go
	Register(handler http.Handler, path string) error
```
to this:
```go
	Register(handler http.Handler, path string, methods ...string) error
```

That new parameter is a list of **HTTP methods**.

This will allow us to use different `http.Handler`s for each **HTTP method** if we want to. For example:
```go
err := router.Register(handleToyDELETE, "/toys", "DELETE")

err := router.Register(handleToyGET, "/toys", "GET")

err := router.Register(handleToyPATCH, "/toys", "PATCH")

err := router.Register(handleToyPUT, "/toys", "PUT")
```

Notice that 4 different `http.Handler` were used in that example.

We also want to make it so, if we want to use an `http.Handler` for all **HTTP methods**, then we can do that with:
```go
err := router.Register(handleSpice, "/spices")

err := router.Register(handleBrick, "/bricks")
```

(Which is what we had in the last section.)

So thus the interface becomes:
```go
interface {
	ServeHTTP(w ResponseWriter, r *Request)
	Register(handler http.Handler, path string, methods ...string) error
}
```

Once you finish that, use the program you wrote to make sure it works.

## 14.6. Summary

So far the HTTP router you created can hand off **HTTP requests** to an `http.Handler` based on an **HTTP path**. For example:
```go
// When an HTTP request for “/apple/banana/cherry” comes in, hand it if off to ‘handleAppleBananaCherry’.
err := router.Register(handleAppleBananaCherry, "/apple/banana/cherry")

// When an HTTP request for “/favorite/fruits” comes in, hand it if off to ‘handleFavoriteFruits’.
err := router.Register(handleFavoriteFruits, "/favorite/fruits")
```

Also, the HTTP router you created can hand off **HTTP requests** to an `http.Handler` based on **HTTP path** and also **HTTP method**. For example:
```go
// When an HTTP request for “GET /toys” comes in, hand it if off to ‘handleToysGET’.
err := router.Register(handleToysGET, "/toys", "GET")

// When an HTTP request for “POST /toys” comes in, hand it if off to ‘handleToysPOST’.
err := router.Register(handleToysPOST, "/toys", "POST")
```

Also you can make a single `http.Handler` response to more than one **HTTP path** and also **HTTP method** combination (but not others). For example:
```go
// When an HTTP request for “DELETE /product”, “GET /product”, “PATCH /product”, or “PUT /product” comes in, hand it if off to ‘handleProduct’.
// But for all other HTTP methods, return a 405 Not Allowed
err := router.Register(handleProduct, "/product", "DELETE", "GET", "PATCH", "PUT")

// When an HTTP request for “GET /product” or “POST /form” comes in, hand it if off to ‘handleForm’.
// But for all other HTTP methods, return a 405 Not Allowed
err := router.Register(handleForm, "/form", "GET", "POST")
```

That's pretty powerful.

## 14.7. Convention Over Configuration

Our `.Register()` method is powerful. But let's improve the user experience with it.

Right now, we have to do things such as:
```go
err := router.Register(handleForm, "/the/form", "G)
```

Your router should have (at least) these methods:
```go
router.Register(handler http.Handler)
router.RegisterPath(handler http.Handler, path string)
router.RegisterPathMethods(handler http.Handler, path string, methods ...string)

```



## 14.8. Extra Points

If you want to make your HTTP router even more powerful, add these features —

### 14.8.1 Delegates

Add this method:
```go
func (receiver *Router) Delegate(handler http.Handler, directory string) error {
	//@TODO
}
```

So that you can do stuff such as:
```go
err := router.Delegate(handleStaticImages, "/images/")
```

Where any path under `/images/` is handed off to `handleStaticImages`. For example, all these (plus more):
* `/images/logo.png`
* `/images/slightly-smiling.png`
* `/images/team/joe.jpeg`
* `/images/team/marry.jpeg`
* `/images/webbug/1x1.gif`

### 14.8.2 Default

Add this method:
```go
func (receiver *Router) Default(handler http.Handler, directory string) error {
	//@TODO
}
```

Where if there is no handler registered or delegated to, then it is called.

[⏮](../http_middleware/README.md)
