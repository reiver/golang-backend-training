# Golang Backend Training

This is a guide to help train someone with backend development using the Go programming language.

If you can accomplish all these tasks, you will have _a lot_ of the skills necessary to do **backend development** using the Go programming language.

THis guide gives you hints. As spend a bit of time trying to figure out yourself. **BUT DON'T SPEND TOO MUCH TIME BEING STUCK. ASK FOR HELP IF YOU GET STUCK!**


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

Create a Go program where you can turn on and off the outputted text.

Use the following variable to switch between text being outputted and text _not_ being outputted.
```Go
var logging bool = true
```

At the beginning of the program log:
> BEGIN

At the end of the program log:
> END

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf) — `fmt.Fprintf()` is similar to `fmt.Printf()` except `fmt.Fprintf()` lets you tell it where to send the output.
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln) — `fmt.Fprintln()` is similar to `fmt.Println()` except `fmt.Fprintln()` lets you tell it where to send the output.
* [os.Stdout](https://golang.org/pkg/os/#Stdout) — `os.Stdout` is where `fmt.Printf()` & `fmt.Println()` send their output.
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)

## 4. Hello {NAME} with logging

Copy your previous _Hello {NAME}_ program, but make it also log the name.

For example, if `name == "Joe"`, then it out log:
> The name was "Joe"

Alternatively, for example, if `name == "Fred"`, then it out log:
> The name was "Fred"

Etc.

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)

## 5. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

## 6. Web Hello {NAME}

Make the API end point `/hello?name=REPLACE_ME` output the following:

`/hello?name=Joe`
```
Hello Joe
```


`/hello?name=Stan`
```
Hello Stan
```
    
Hint:
* [fmt.Fprintf](https://golang.org/pkg/fmt/#Fprintf)

## 7. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

## 6. Web Hello {NAME} with JSON

Copy your previous _Web Hello {NAME}_ program, but make it output JSON:


I.e., make the API end point `/hello?name=REPLACE_ME` output the following:

`/hello?name=Joe`
```json
{
    "msg":"Hello Joe!"
}
```


`/hello?name=Stan`
```json
{
    "msg":"Hello Stan!"
}
```
