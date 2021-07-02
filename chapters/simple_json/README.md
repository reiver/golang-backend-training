## 6. Simple JSON

### 6.1. Simple JSON

Using the built-in `"encoding/json"`package to return an HTTP response whose payload is JSON can be quite verbose, with a lot of biolerplate looking code.

To make the _developer user experience_ better we are going to look the `simplehttp` package:

https://github.com/reiver/go-simplehttp

With this, instead of writing:
```go

import "encoding/json"

// ...

func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	w.Header().Set("Content-Type", "application/json")
	w.WriteHeader(http.StatusNotFound)
	err := json.NewEncoder(w).Encode(struct{
		StatusCode int64  `json:"status_code"`
		StatusName string `json:"status_name"`
	}{
		StatusCode: http.StatusNotFound,
		StatusName: "Not Found",
	})
	if nil != err {
		// ...
	}
}


```
We can write:
```go

import "github.com/reiver/go-simplehttp"

// ...

simplejson, err := simplehttp.Load("json")

// ...

func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	simplejson.NotFound(w)
}
```

Re-write that API end point that accepts two numbers, adds then, and outputs the result, so that it uses the `simplehttp` package to return the result. I.e.,:

`/addition?x=3&y=2`
```
{
    "result":"5",
}
```

Hints:
* [strconv.ParseInt()](https://golang.org/pkg/strconv/#ParseInt)
* [strconv.ParseUint()](https://golang.org/pkg/strconv/#ParseUint)
* [import "github.com/reiver/go-simplehttp"](https://pkg.go.dev/github.com/reiver/go-simplehttp)

-----

[RETURN](../../README.md)
