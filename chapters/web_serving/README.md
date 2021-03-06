# 5. WEB SERVING ([Golang Backend Training](../../README.md))

## 5.1. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Also include logging.

And note, if you use `http.ListenAndServe()` the 2nd parameter should NOT be nil. An `http.Handler` should be passed in with the 2nd parameter.

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

## 5.2. Web Hello {NAME}

Make the API end point `/hello?name=REPLACE_ME` output the following:

`/hello?name=Joe`
```
Hello Joe
```


`/hello?name=Stan`
```
Hello Stan
```
Also include logging.

And note, if you use `http.ListenAndServe()` the 2nd parameter should NOT be nil. An `http.Handler` should be passed in with the 2nd parameter.

Hint:
* [fmt.Fpricntf](https://golang.org/pkg/fmt/#Fprintf)
* [http.Handler](https://golang.org/pkg/net/http/#Handler)
* [http.ResponseWriter](https://golang.org/pkg/net/http/#ResponseWriter)

-----


[⏮](../logging/README.md) [⏭️](../json/README.md)
