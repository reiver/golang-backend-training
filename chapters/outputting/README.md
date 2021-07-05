# 1. Outputting ([Golang Backend Training](../../README.md))

## 1.1. Hello world!

Create a Go program that outputs the text:
> Hello world!

Hints:
* [fmt.Println()](https://golang.org/pkg/fmt/#Println)
* [installing Go](https://golang.org/doc/install)
* [getting started with Go](https://golang.org/doc/tutorial/getting-started)
* [A Tour of Go](https://tour.golang.org/)

## 1.2. go run

Run your program using `go run`

So, for example, if all your source code is in the one file `main.go`, then you would run:
```
go run main.go
```

**Use `go run` to run the _Hello world!_ program you previously created.**

Did it output?:
> Hello world!

## 1.3. go build

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

➤ Note that if you are using `git`, typically most people do NOT commit executable files into git. So you probably want to be careful with what you commit. Maybe even exclude the executable file using a `.gitignore` file.

## 1.4. Hello {NAME}

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

## 1.5. Form Letter

Let's now make it so we are saying more than just _“Hello”_. Let's make it so the program says something such as:

> Hello Joe!
> 
> The weather today is sunny.
> 
> Today's snack will be french fries.

Or:

> Hello Fred!
> 
> The weather today is cloudy.
> 
> Today's snack will be meatloaf.

And have it so the person's name (ex: _“Joe”_, _“Fred”_, etc) is stored in a variable; for example:
```go
var name string = "John"
```

Have it so the type of weather is also stored in a variable; for example:
```go
var weather string = "raining"
```

And finally have it so the snack is too stored in a variable; for example:
```go
var snack string = "macaroni and cheese"
```

After you have done that, do a go build, and make sure you get what is expected.

## 1.6. Form Letter Func

Let's organize your code a bit. Let's make it so that the code that outputs the _form letter_ is in a function.

And make it so the _name_, _weather_, and _snack_ are passed to this function as parameters.

After you have done that, do a go build, and make sure you get what is expected.

Hints:
* [Go by Example: Functions](https://gobyexample.com/functions)
* [A Tour of Go: Functions](https://tour.golang.org/basics/4)
* [A Tour of Go: Functions continued](https://tour.golang.org/basics/5)
* [A Tour of Go: Multiple results](https://tour.golang.org/basics/6)
* [A Tour of Go: Named return values](https://tour.golang.org/basics/7)

## 1.7. Configurations File

These variables — `name`, `weather`, and `snack` — operate as _configuration parameters_.

Let's move them into their own file so that it is easier to locate them and potentially edit them.

So, let's make it so your program has 2 files:

* main.go
* cfg.go

➤ `cfg` is short for _“configurations”_ or _“configuration parameters”_ (depending on who you ask).

In `cfg.go` let's put those 3 variables: `name`, `weather`, and `snack`

After you have done that, do a `go build`, and make sure you get the same output as before.

## 1.8. Form Letter File

Let's further organization our code by putting the form letter func into its own file too. So that you code's file structure would be:

* main.go
* cfg.go
* formletter.go

After you have done that, do a `go build`, and make sure you get the same output as before.

# 1.9. Form Letter Package

Let's move the _form letter_ function into its own sub-directory package.

So, you will have:

* main.go
* cfg.go
* lib/
  * formletter/
    * formletter.go

I.e., the `formletter.go` file will be moved to:
```
lib/formletter/formletter.go
```

You should change the package name of this file to:
```go
package formletter
```

And then import it from your `main.go`

After you have done that, do a `go build`, and see if you get the same output as before.

Actually, **it won't work!**

The reason is that `package main` imports `package formletter`, but `package formletter` needs the configuration parameters in the `cfg.go` file from `package main`.

I.e., you have circular dependencies. Which Go doesn't permit.

Thus, you need to move the configuration parameters to its own sub-directory package too.

➤ It is usually a good idea to put the _configuration parameters_ into their own sub-directory package — such as `cfg/`

So, let's make the file layout look like:

* main.go
* cfg/
  * cfg.go
* lib/
  * formletter/
    * formletter.go

Once you make that change, it should work.

After you have done that, do a `go build`, and make sure you get the same output as before.

-------------------------

[⏮](../../README.md) [⏭️](../flagging/README.md)
