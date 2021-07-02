## 1. Outputting

### 1.1. Create a Go program that outputs text

Create a Go program that outputs the text:
> Hello world!

Hints:
* [fmt.Println()](https://golang.org/pkg/fmt/#Println)
* [installing Go](https://golang.org/doc/install)
* [getting started with Go](https://golang.org/doc/tutorial/getting-started)
* [A Tour of Go](https://tour.golang.org/)

### 1.2. go run

Run your programing using `go run`

So, for example, if all your source code is in the one file `main.go`, then you would run:
```
go run main.go
```

**Use `go run` to run the _Hello world!_ program you previously created.**

Did it output?:
> Hello world!

### 1.3. go build

Using `go run` can be quick when we are able to use it.

But we cannot use `go run` to create an executable program from our source code. Also, `go run` won't work with some code layouts!

Either way, to create an executable program, we run `go build`

Unlike `go run` you don't need to specify the your `.go` file(s). You just need to run it from the same directory your `.go` files are in.

So you would just run:
```
go build
```

By default the executable file that `go build` creates will have the same name as the directory.

So, for example, if your source code is in a directory names `backoffice123/`, then by default the executable `go build` creates will be named `backoffice123`.  And if the directory is named `ch3rry/`, then by default  the executable `go build` creates will be named `ch3rry`

If you want the executable file `go build`  creates to be named something different than the directory name, then use the `-o` flag. For example:
```go
go build -o myprogramname
```

**Use `go build` to create an executable file from the _Hello world!_ program you previously created, and then run that executable file.**

Did it output?:
> Hello world!

### 1.4. Hello {NAME}

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

-------------------------

[RETURN](../README.md)
