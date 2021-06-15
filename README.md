# Golang Backend Training

This is a guide to help train someone with backend development using the Go programming language.

## 1. Create a Go program that outputs text

Create a Go program that outputs the text:
> Hello world!

Hints:
* [fmt.Println()](https://golang.org/pkg/fmt/#Println)

## 2. Hello {NAME}

Create a Go program that takes a name from a variable:
```Go
var name string = "Joe"
```
Or:
```Go
var name string = "Fred"
```
Or whatever.

And outputs a message such as:
```
Hello Joe!
```
Or:
```
Hello Fred!
```
Or whatever, depending on the value of the `name` variable.

Hints:
* [fmt.Printf()](https://golang.org/pkg/fmt/#Printf)

## 3. Create a simple logger

Create a Go program where you can turn on and off the outputted text:

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln)
* [os.Stdout](https://golang.org/pkg/os/#Stdout)
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)


## 4. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)


## 5. Hello {NAME}

Make the API end point `/hello?name=REPLACE_ME` output the following:

`/hello?name=Joe`
```
Hello Joe
```


`/hello?name=Stan`
```
Hello Stan
```

I.e., make it so
    
Hint:
* [fmt.Fprintf](https://golang.org/pkg/fmt/#Fprintf)

## 6. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

    
Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)
