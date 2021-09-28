# 4. Logging ([Golang Backend Training](../../README.md))
by [Charles Iliya Krempeaux](http://changelog.ca/)
-----

In this chapter you will create a **logger**.

Loggers let programmers record information about events that happen when the program is running.

So, for example:
```go
log.Alert("The super-user just logged in!")
```

Typically the programmer is reading the logs, not the end user. I.e., the logs are there to help **you**!

Logs can help you debug your code while you are doing your software development work, and, if there is a problem on production, logs can also help you figure out what went wrong on production.

(Logs can also be read by software programs for monitoring, to detect hack attempts, etc.)

At first your logger will be simple. But we will keep adding to it until it is quite powerful & sophisticated.

## 4.1. Create a simple logger

Let's start by №1 creating a simple logger, and then №2 creating a (very simple) program that uses that logger.

The program you will create (that uses that logger you created) will log the following:—

At the beginning of the program it will log:
> BEGIN

In the middle of the program it will log:
> I said "Hello world!"

And at the end of the program it will log:
> END

And it will look something like:
```
package main

func main() {
	log.Begin()
    
	var msg string = "Hello world!"
	fmt.Println(msg)
	log.Log("I said:", msg)
    
	log.End()
}
```

The logger you create will be represents by a type:
```
type Logger struct {
    //@TODO: you will need to figure out what goes here.
}
```

This logger will provide methods to output text BUT **you will write it in a way that you have the ability to turn on and off the outputted text, and decide where you want the output to go**.

The first method your logger will have is:
```
func (receiver Logger) Log(a ...interface{}) {
    //@TODO: you will need to figure out what goes here.
}
```
The other two methods your logger will have are:
```
func (receiver Logger) Begin() {
    //@TODO: you will need to figure out what goes here.
}
```

```
func (receiver Logger) End() {
    //@TODO: you will need to figure out what goes here.
}
```

These other two methods should use the `.Log()` method (you created before) to do their outputting.


Hints:
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln) — `fmt.Fprintln()` is similar to `fmt.Println()` except `fmt.Fprintln()` lets you tell it where to send the output.
* [os.Stdout](https://golang.org/pkg/os/#Stdout) — `os.Stdout` is where `fmt.Printf()` & `fmt.Println()` send their output.
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)
* [Quick-and-Dirty Debugging in Golang](https://changelog.ca/log/2015/03/09/golang)

## 4.2. Hello {NAME} with logging

Copy your previous _Hello {NAME}_ program, but make it also log the name (in addition to ading `.Begin()` & `.End()`).

For example, if `name == "Joe"`, then it logs:
> The name was "Joe"

Alternatively, for example, if `name == "Fred"`, then it out log:
> The name was "Fred"

Etc.

So, because you are also calling the `.Begin()` & `End()` functions, then your full output will be something like:
```
BEGIN
The name is "Joe"
Hello Joe!
END
```

Note that 3 of those lines are output from logs; and 1 of those lines is regular output.

This is a **log**:
> `BEGIN`

This is a **log**:
> `The name is "Joe"`

This is regular output:
> `Hello Joe!`

And this is a **log**:
> `END`


To accomplish this you should add another method to your logger:
```
func (receiver Logger) Logf(format string, a ...interface{}) {
    //@TODO:  you will need to figure out what goes here.
}
```

Such that when you log the name you do a:
```
log.Logf("The name was %q", name)
```

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)

## 4.3. Repository "go-log"

Create a new publicly accessible repository named `go-log`.

If you are on [GitHub](https://github.com/) and your username is `joeblow`, then you would create:
```
https://github.com/joeblow/go-log
```

If you are on [Bitbucket](https://bitbucket.org/) and your username is `homersimpson`, then you would create:
```
https://bitbucket.org/homersimpson/go-log
```

If you are on [Gitlab](https://gitlab.com/) and your username is `commanderkeen`, then you would create:
```
https://gitlab.com/commanderkeen/go-log
```

Etc.

## 4.4. Pacakge "log"

Put your logger code into the `go-log` repository you previously created.

The name of your package will be `log`. I.e.,:—
```go
package log
```

➤ You might have noticed that the repository is called `go-log`, but the package is named `log`. That is on purpose. The convention in the Go community is to name things this way.

### 4.5. Unit Testing

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

So, for example, if we are testing the `Logf()` method of the type `Logger` we might name our test:
```go
func TestLogger_Logf(t *testing.T) {
	//@TODO
}
```

And, for example, if we are testing the `Punch()` function, we might name our test:
```go
func TestPunch(t *testing.T) {
	//@TODO
}
```

And if we wanted to have 2 different tests for `the Log()` method we might have the following:
```go
func TestLogger_Log_apple(t *testing.T) {
	//@TODO
}

func TestLogger_Log_banana(t *testing.T) {
	//@TODO
}

func TestLogger_Log_cherry(t *testing.T) {
	//@TODO
}
```

Etc.

To run your unit tests, you will use the following command from the command line:
```
go test
```

The output from running this program will tell you if any tests failed.

**Write units tests to make sure your logger is working as you expect it to work.**

You will need to figure out how to capture the output from your `Log()` and `Logf()` functions. You can use [strings.Builder](https://golang.org/pkg/strings/#Builder) to do this; as a pointer to [strings.Builder](https://golang.org/pkg/strings/#Builder) is an `io.Write` — i.e.,:—
```go
var output strings.Builder

var writer io.Writer = &output
```

Hints:
* [Go by Example: Testing](https://gobyexample.com/testing)
* [Add a Test](https://golang.org/doc/tutorial/add-a-test)
* [Table Driven Tests](https://github.com/golang/go/wiki/TableDrivenTests)
* [import "testing"](https://golang.org/pkg/testing/)
* [strings.Builder](https://golang.org/pkg/strings/#Builder)

## 4.6. import "go-log"

Write a program that uses your `"log"` package.

At the beginning of the program log:
> BEGIN

At the end of the program log:
> END
(Of better yet, use Go's `defer` keyword for _END_.)

And in the middle of the program, log:
> I am here!

## 4.7. Verbose

Write a program that normally discards all the logs. But if the `-v` flag is sent to it, then it will output the logs.

So, if you program was named `myprogram`, then running:
```
myprogram
```
Would output nothing.

But running:
```
myprogram -v
```
Would output:
```
BEGIN
END
```

Hints:
* [import "flag"](https://golang.org/pkg/flag/)

## 4.8. Prefix

Modify the logger you created so that it has this method:
```go
func (receiver Logger) Prefix(newprefix ...string) Logger {
	//@TODO
}
```

So that if we had:
```go
package main

// ...

func main() {
	prefixedLogger := log.Prefix("apple", "banana", "cherry")

	prefixedLogger.Log("Hello world!")
	
	doublePrefixedLogger := prefixedLogger.Prefix("date")
	
	doublePrefixedLogger.Log("I am here!")
}
```
It would output something similar to:
```
apple: banana: cherry: Hello world!
apple: banana: cherry: date: I am here!
```

## 4.9. Begin Prefix

Modify the `.Begin()` function you created before so that it accepts the same type of parameters as `.Prefix()`; i.e.,:
```go
func (receiver Logger) Begin(newprefix ...string) Logger {
	//@TODO
}
```

So that if we had:
```go
package main

// ...

func main() {
	lg := log.Begin("apple", "banana", "cherry")

	lg.Log("Hello world!")
	
	plog := lg.Prefix("date")
	
	plog.Log("I am here!")

	log.End()
}
```
It would output something similar to:
```
apple: banana: cherry: BEGIN
apple: banana: cherry: Hello world!
apple: banana: cherry: date: I am here!
apple: banana: cherry: END
```


## 4.10. Func Name

Modify the logger you created so that when you call `.Begin()` it figures out what function it was called it, and stores the that information in the **new** logger it created, so that when `Log()`, `Logf()` and `.End()` are called using it, the function name comes before the prefix.

So, for example, this program:
```go
package main

// ...

func main() {
	log := logsrv.Begin().Prefix("apple", "banana", "cherry")
	defer log.End()
	
	log.Log("Howdy!")
}
```
Would output something similar to:
```
main: BEGIN
main: Howdy!
main: END
```

If you are confused by the `defer` statement, that program is similar to this one:
```go
package main

// ...

func main() {
	log := logsrv.Begin().Prefix("apple", "banana", "cherry")
	
	log.Log("Howdy!")

	log.End()
}
```
(Note that `log.End()` moved to the bottom of the `main()` function.)


Hints:
* [runtime.Callers()](https://golang.org/pkg/runtime/#Callers)
* [runtime.FuncForPC()](https://golang.org/pkg/runtime/#FuncForPC)
* [runtime.Func.Name()](https://golang.org/pkg/runtime/#Func.Name)


## 4.11. Timer

We want to make it so calling `.End()` will also output the value of a timer that was started when we called `.Begin()`

So that a program such as this:
```go
package main

// ...

func main() {
	log.Begin()
	
	log.End()
}
```
Would output something similar to:
```
main: BEGIN
main: END δt=15µs
```

To do this we are going to have to radically change how `.Begin()` and `.End()` work.

We need to make it so calling `.Begin()` №1 still outputs what it did before but now №2 returns a new logger. I.e.,:—
```go
sublogger := log.Begin()
```

And then when we call `.End()` it is (not on the original logger but) on this new logger. I.e.,:—
```go
sublogger.End()
```

So, a more full example might be:
```go
locallogger := log.Begin()

locallogger.Logf("The name is %q", name)
fmt.Printf("Hello %s!\n", name)

locallogger.End()
```

**Make this change, and then create a program that uses them.**

Hints:
* [time.Time](https://golang.org/pkg/time/#Time)
* [time.Now()](https://golang.org/pkg/time/#Now)

## 4.12. Leveled Logger

Sometimes it is useful to have a logger that can categorize its logs, and turn on and off the different categories of logs.

Change your logger to have these levels:
```go
type Logger interface {
	Alert(a ...interface{})
	Alertf(format string, a ...interface{})

	Error(a ...interface{})
	Errorf(format string, a ...interface{})
	
	Highlight(a ...interface{})
	Highlightf(format string, a ...interface{})

	Inform(a ...interface{})
	Informf(format string, a ...interface{})

	Log(a ...interface{})
	Logf(format string, a ...interface{})

	Trace(a ...interface{})
	Tracef(format string, a ...interface{})
	
	Warn(a ...interface{})
	Warnf(format string, a ...interface{})
	
	Prefix(...string) Logger
	
	Begin() Logger
	
	End()
	
	Level(uint8) Logger
}
```

And make it so that your logger has a concept of a “level”.

* level 0 — _nothing_ is outputted
* level 1 — only **alert**, and **error** are outputted
* level 2 — everything from level 1 is outputted, plus **warn** is also outputted
* level 3 — everything from level 2 is outputted, plus **highlight** is also outputted
* level 4 — everything from level 3 is outputted, plus **inform** is also outputted
* level 5 — everything from level 4 is outputted, plus **log** is also outputted
* level 6 — everything from level 5 if outputted, plus **trace** is also outputted

Use the `Level()` method to handle these levels.

Also, make it so anything above level 6 — 7, 8, 9, 10, etc … — acts the same as level 6. I.e., all the logs are on.

## 4.13. Leveled Logger Unit Tests

Add to your unit tests to cover all these new methods.

## 4.14. Leveled Logger Demonstration

Write a program that uses your leveled logger, and use each level in the appropriate way.

Your default choice should be `Log()` & `Logf()`

If you want to dump the contents of a "large" data structure or variable, then you should use `Trace()` & `Tracef()`; for example:
```go
func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	log.Trace("HTTP request:", r)

	// ...
}
```
And:
```go
var users []User

// ...

for i, user := range users {
	log.Trace("user ", i, "is", user)
}
```

If you have information that you want to record that is a bit more important than a regular log, then you should use `Inform()` & `Informf()`; for example:
```go
func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	lg := log.Begin()

	lg.Log("Receive HTTP Request")
	lg.Trace("HTTP request:", r)

	// ...
	lg.Log("Tried to INSERT into database.")

	// ...
	lg.Inform("new user created") // <----

	lg.End()
}
```
If you have information that you want to record that you want to highlight above the regular logs then use `Highlight()` & `Highlightf()`

If an error occurred then use `Error()` & `Errorf()`; for example:
```go
	lg := log.Begin()
	
	// ...

	err := something.DoIt()
	if nil != err {
		log.Error("problem doing it:", err) // <----
		return err
	}
	log.Log("Success! — was able to do it.")
	
	// ...
	
	lg.End()
```

## 4.15. Logger Verbosity

Make it so your program can turn on an off different levels of logs using _logger verbosity flags_.

So, if your executable file is names `myprogram`, then —

Running this:
```
myprogram
```
… would output no logs.

Running this:
```
myprogram -v
```
… would output output the **level 1** logs.


Running this:
```
myprogram -vv
```
… would output output the **level 2** logs.

Running this:
```
myprogram -vvv
```
… would output output the **level 3** logs.

Running this:
```
myprogram -vvvv
```
… would output output the **level 4** logs.

Running this:
```
myprogram -vvvvv
```
… would output output the **level 5** logs.

Running this:
```
myprogram -vvvvvv
```
… would output output the **level 6** logs.


You code layout will have:

* main.go
* arg/
  * arg.go 
* srv/
  * log/
    * log.go  

These `-v`, `-vv`, `-vvv`, `-vvvv`, `-vvvvv`, and `-vvvvvv` flags will be handled in `arg/arg.go`

`srv/log/log.go` will import that `flags` package to figure out what level it should set itself to.

The `srv/log` package should only export on thing, a `Begin()` function — i..,:
```go
logsrv.Begin()
```
So that you can do stuff such as:
```go
func MyFunction() {
	log := logsrv.Begin()
	defer log.End()
	
	// ...
	
	log.Alert("Hello world!")
	
	// ...
}
```


## 4.16. License

Add a `LICENSE` file to your `go-log` repository.

Your are going to use this for you job, so it **must** be a business-friendly license.

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

## 4.17. README.md

Add a `README.md` file to you `go-log` repository.

Make it include a URL to online documentation for your package, using https://pkg.go.dev/


## 4.18. Documentation

Notice that the online documentation for your package at https://pkg.go.dev/ doesn't have any descriptions or examples (like the documentation you see for many of the Go built-in packages).


Add documentation to your `log` package.


-----

[⏮](../interfaces/README.md) [⏭️](../web_serving/README.md)
