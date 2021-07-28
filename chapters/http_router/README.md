# 14. HTTP Router ([Golang Backend Training](../../README.md))

In this chapter you are going to create an **HTTP router**.

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

The `http.ListenAndServe()` function (from Go's built-in `"net/http"` package) will call your `theHandlerYouCreated.ServerHTTP()` method for **all** HTTP requests. All of them!
Doesn't matter the **HTTP path** is. Doesn't matter what the **HTTP method** is. All HTTP requests will be handed off to your `theHandlerYouCreated.ServerHTTP()` method!

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

## 14.2. HTTP Router

The first thing to realize is that an **HTTP router** is also an `http.Handler`

That means that the **HTTP router** you create will have a `.ServeHTTP(http.ResponseWriter, *http.Request)` method.

So your **HTTP router** will look something like:
```go
package httprouter

type Router struct {
	//@TODO
}

func (receiver Router) ServeHTTP(http.ResponseWriter, *http.Request) {
	//@TODO
}

//@TODO: more methods, etc
```

## 14.2. Simple HTTP Router

First, you are going to create a _simple_ **HTTP router**.

This _simple_ **HTTP router** will do things such as letting you specify what `http.Handler` should be called for a specific **HTTP path** + **HTTP method** pair.

For example, something like this:

* `GET /apple/banana/cherry` -> handler1
* `PATCH /apple/banana/cherry` -> handler2
* `GET /some/path` -> handler3
* etc

## 14.1. Handler Interface

Implement an **HTTP router** using this interface:
```go
type HTTPRouter interface {
	AutoDelegate(handler http.Handler) error
	AutoRegister(handler http.Handler, methods ...string) error

	Delegate(handler http.Handler, path string) error
	Register(handler http.Handler, path string, methods ...string) error
}
```

## 14.2. Convention Over Configuration

We are going to add two more methods to our `HTTPRouter` interface:
```go
AutoDelegate(handler http.Handler) error
AutoRegister(handler http.Handler, methods ...string) error
```
So that we have:
```go
type HTTPRouter interface {
	AutoDelegate(handler http.Handler) error
	AutoRegister(handler http.Handler, methods ...string) error

	Delegate(handler http.Handler, path string) error
	Register(handler http.Handler, path string, methods ...string) error
}
```

What `AutoDelegate()` and `AutoRegister()` do is —

`AutoDelegate()` is similar to `Delegate()` except that the caller does NOT specify the `path`, but instead `AutoDelegate()` infers the path
