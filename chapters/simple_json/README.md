# 7. Simple JSON
by [Charles Iliya Krempeaux](http://changelog.ca/)
-----

## 7.1. Marshal JSON — json.Marshal()

Go comes with a built-in library for working with JSON — `"encoding/json"` You can see the API for this Go library at the following URL:

https://pkg.go.dev/encoding/json


One can, for example, turn a Go `map[string]interface{}` into JSON with Go code similar to the following:
```go
import "encoding/json"

// ...

var data map[string]interface{} = map[string]interface{}{
	"apple":"ONE",
	"banana":"TWO",
	"cherry":"THREE",
}

// ...

p, err := json.Marshal(data)
```

In this code `p` is a `[]byte` that has the JSON in it.

This will Go code will (logically) result in the following JSON code:
```json
{
	"apple":"ONE",
	"banana":"TWO",
	"cherry":"THREE",
}
```

The `json.Marshal()` function can also marshal other Go datatypes.
For example, here is the marshaling of a Go `struct` into JSON:
```go
p, err := := json.Marshal(struct{
	Apple bool    `json:"aplpe"`
	Banana string `json:"banana"`
	Cherry int64  `json:"cherry"`
	}{
		Apple: true,
		Banana: "TWO",
		Cherry: 3,
	}
})
```
This will (logically) result in the following JSON code:
```json
{
	"apple":true,
	"banana":"TWO",
	"cherry":3
}
```

## 7.2. Marshal JSON — json.NewEncoder().Encode()

One common time that a Go programmer would write JSON marshaling code is when he or she is responding to an HTTP request.
I.e., when creating an HTTP response.

Since an `http.ResponseWriter` fits the `io.Writer` interface, instead of using `json.Marshal()` to turn data in Go into JSON, we could instead use `json.NewEncoder().Encode()` to simplify things for ourselves. So for a non-HTTP example of using `json.NewEncoder().Encode()`:
```go
var jsonGoesHere strings.Builder

var writer io.Writer = &jsonGoesHere

err := json.NewEncoder(writer).Encode(struct{
	GivenName     string  `json:"given_name"`
	AdditionNames string `json:"additional_names"`
	FamilyName    string `json:"family_name"`
}{
	GivenName:"Joe",
	FamilyName: "Blow"
})
if nil != err {
	// ...
}
```
This will (logically) result in the following JSON code:
```json
{
	"given_name":"Joe",
	"additional_names":"",
	"family_name":"Blow",
}
```

## 7.3. HTTP Response

Let's now marshal Go data into JSON **as the body of an HTTP response**.
And let's use `json.NewEncoder().Encode()` (rather than `json.Marshal()`) to make it happen.

So an example of what that might look like is the following:
```go
import (
	"encoding/json"
	"io"
}

// ...

func (receiver T) ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	w.Header().Set("Content-Type", "application/json")
	w.WriteHeader(http.StatusNotFound)
	err := json.NewEncoder(w).Encode(struct{
		StatusCode   int64  `json:"status_code"`
		StatusName   string `json:"status_name"`
		HumanMessage string `json:"message"`
	}{
		StatusCode: http.StatusNotFound,
		StatusName: "Not Found",
		HumanMessage: "This is not the URI you are looking for.",
		
	})
	if nil != err {
		// ...
	}

	// ...
}
```

This will (logically) result in the following JSON code:
```json
{
	"status_code":404,
	"status_name":"Not Found",
	"human_message": "This is not the URI you are looking for."
}
```

That Go code is a lot of code for just wanting to return a `404 Not Found` HTTP response with a JSON body.

Let's create a better **developer user-experience** (**UX**) for ourserlves, and anyone else who might use our code.

## 7.4. httpjson

We are going to turn the previous code into code similar to the following:
```go
func (receiver T) ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	data := struct{
		StatusCode   int64  `json:"status_code"`
		StatusName   string `json:"status_name"`
		HumanMessage string `json:"human_message"`
	}{
		StatusCode: http.StatusNotFound,
		StatusName: "Not Found",
		HumanMessage: "This is not the URI you are looking for.",
	}

	httpjson.NotFound(w, data)
	
	// ...
}
```

Note that the code that turns that Go data-type into JSON, and sends the HTTP response is just this one line of code:
```go
httpjson.NotFound(w, data)
```

That is a huge improvement over what we had before!


The HTTP protocol has a lot of different built-in HTTP responses. We are going to handle _all_ of them as we implement our `httpjson` package.

## 7.4. Repository "go-httpjson"

Create a new public repo called `go-httpjson`

If you are on GitHub, and your username was `joeblow`, then you would be creating:

`https://github.com/joeblow/go-httpjson`

If you are on Gitlab, and your username was `janedoe`, then you would be creating:

`https://gitlab.com/janedoe/go-httpjson`

Etc.

## 7.5. License

Add a `LICENSE` file to your `go-httpjson` repository.

You are going to use this for you job, so it **must** be a business-friendly license.

I suggest you use the **MIT license**:

> Copyright {YEAR} {COPYRIGHT HOLDER}
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

So, for example, if your name is **“Joe Blow”**, and the year is **“2021”**, then your `LICENSE` file might be:

> Copyright 2021 Joe Blow
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## 7.6. README.md File

Add a `README.md` file to you `go-httpjson` repository.

Make it include a URL to online documentation for your package, using https://pkg.go.dev/

## 7.7. Package "httpjson"

In that new repository, you are going to name the new package:
```go
package httpjson
```


And, for now, you are going to implement the following functions:
```go
package httpjson

OK(http.ResponseWriter, ...interface{})       // 200 OK
Accepted(http.ResponseWriter, ...interface{}) // 202 Accepted

BadRequest(http.ResponseWriter, ...interface{})                   // 400 Bad Request
Unauthorized(http.ResponseWriter, ...interface{})                 // 401 Unauthorized

Forbidden(http.ResponseWriter, ...interface{})                    // 403 Forbidden
NotFound(http.ResponseWriter, ...interface{})                     // 404 Not Found
MethodNotAllowed(http.ResponseWriter, ...interface{})             // 405 Method Not Allowed

InternalServerError(http.ResponseWriter, ...interface{})     // 500 Internal Server Error
```

Although long-term we are going to implement all of these:
```go
package httpjson

OK(http.ResponseWriter, ...interface{})       // 200 OK
Accepted(http.ResponseWriter, ...interface{}) // 202 Accepted

BadRequest(http.ResponseWriter, ...interface{})                   // 400 Bad Request
Unauthorized(http.ResponseWriter, ...interface{})                 // 401 Unauthorized
PaymentRequired(http.ResponseWriter, ...interface{})              // 402 Payment Required
Forbidden(http.ResponseWriter, ...interface{})                    // 403 Forbidden
NotFound(http.ResponseWriter, ...interface{})                     // 404 Not Found
MethodNotAllowed(http.ResponseWriter, ...interface{})             // 405 Method Not Allowed
NotAcceptable(http.ResponseWriter, ...interface{})                // 406 Not Acceptable
ProxyAuthRequired(http.ResponseWriter, ...interface{})            // 407 Proxy Authentication Required
RequestTimeout(http.ResponseWriter, ...interface{})               // 408 Request Timeout
Conflict(http.ResponseWriter, ...interface{})                     // 409 Conflict
Gone(http.ResponseWriter, ...interface{})                         // 410 Gone
LengthRequired(http.ResponseWriter, ...interface{})               // 411 Length Required
PreconditionFailed(http.ResponseWriter, ...interface{})           // 412 Precondition Failed
RequestEntityTooLarge(http.ResponseWriter, ...interface{})        // 413 Request Entity Too Large
RequestURITooLong(http.ResponseWriter, ...interface{})            // 414 Request-URI Too Long
UnsupportedMediaType(http.ResponseWriter, ...interface{})         // 415 Unsupported Media Type
RequestedRangeNotSatisfiable(http.ResponseWriter, ...interface{}) // 416 Requested Range Not Satisfiable
ExpectationFailed(http.ResponseWriter, ...interface{})            // 417 Expectation Failed
Teapot(http.ResponseWriter, ...interface{})                       // 418 I'm a teapot

InternalServerError(http.ResponseWriter, ...interface{})     // 500 Internal Server Error
NotImplemented(http.ResponseWriter, ...interface{})          // 501 Not Implemented
BadGateway(http.ResponseWriter, ...interface{})              // 502 Bad Gateway
ServiceUnavailable(http.ResponseWriter, ...interface{})      // 503 Service Unavailable
GatewayTimeout(http.ResponseWriter, ...interface{})          // 504 Gateway Timeout
HTTPVersionNotSupported(http.ResponseWriter, ...interface{}) // 505 HTTP Version Not Supported
```

But you can implement functions from the full-list whenever you end up needing them.)

So, implement the 8 functions in the first list as `package httpjson`.

# 7.8. Unit Testing

**Unit testing** are tests used to test a piece of a software system. (These _pieces_ of the software system get called _“units”_ — thus the name “unit test”.)

Go has built-in support for **unit testing**.

With Go, _unit tests_ are put in files that end in `_test.go`

So, for example, you might have a unit test file name: `apple_test.go`, `banana_test.go`, and `cherry_test.go`, and even `one_two_three_test.go`

(When you normally build a program — using `go build` — all the `*_test.go` are ignored. Go only pays attention to the `*_test.go` files when it runs the tests — when you run `go test`)

All Go unit tests will need to import the ["testing"](https://golang.org/pkg/testing/) package:
```go
import "testing"
```

Inside the `*_test.go` file, each test is put inside a function whose name starts with `Test`.

So, for example, if we are testing the `OK()` function then we might name our test:
```go
func TestOK(t *testing.T) {
	//@TODO
}
```

And, for example, if we are testing the `NotFound()` function, we might name our test:
```go
func TestNotFound(t *testing.T) {
	//@TODO
}
```

And if we wanted to have 3 different tests for the `NotFound()` function we might have the following:
```go
func TestNotFound_success(t *testing.T) {
	//@TODO
}

func TestNotFound_Log_failure(t *testing.T) {
	//@TODO
}

func TestNotFound_Log_bug123(t *testing.T) {
	//@TODO
}
```

Etc.

To run your unit tests, you will use the following command from the command line:
```
go test
```

The output from running this program will tell you if any tests failed.

**Write units tests to make sure your httpjson functions are working as you expect it to work.**


Hints:
* [Go by Example: Testing](https://gobyexample.com/testing)
* [Add a Test](https://golang.org/doc/tutorial/add-a-test)
* [Table Driven Tests](https://github.com/golang/go/wiki/TableDrivenTests)
* [import "testing"](https://golang.org/pkg/testing/)
* [strings.Builder](https://golang.org/pkg/strings/#Builder)

## 7.9. Documentation

Notice that the online documentation for your package at https://pkg.go.dev/ doesn't have any descriptions or examples (like the documentation you see for many of the Go built-in packages).

Add documentation to your `httpjson` package.

## 7.10. Use It

You are now going to use your new `httpjson` package.

You are going to create this API end point:

```
/subtract?x=5&y=4
```

Such that this would return this:
```json
{
	"result":3
}
```

Where you use your new `httpjson` package to return the result. I.e.,:
```go
httpjson.OK(w, result)
```

Hints:
* [strconv.ParseInt()](https://golang.org/pkg/strconv/#ParseInt)
* [strconv.ParseUint()](https://golang.org/pkg/strconv/#ParseUint)
* [import "github.com/reiver/go-simplehttp"](https://pkg.go.dev/github.com/reiver/go-simplehttp)

-----
