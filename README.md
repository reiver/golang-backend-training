# Golang Backend Training

This is a guide to help train someone with backend development using the Go programming language.

## 1. Create a Go program that outputs text

Create a Go program that outputs the text:
> Hello world!

Hints:
* [fmt.Println()](https://golang.org/pkg/fmt/#Println)

## 2. Create a simple logger

Create a Go program where you can turn on and off the outputted text:

Hints:
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln)
* [os.Stdout](https://golang.org/pkg/os/#Stdout)
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)

## 3. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

## 4. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)
