## 3. Logging

### 3.1. Create a simple logger

In this section you will №1 create a logger, and then №2 create a (very simple) program that uses that logger.

(Loggers let programmers record information about events.)

The program you will create (that uses that logger you created) will log the following:—

At the beginning of the program it logs:
> BEGIN

At the end of the program it logs:
> END

And it will look something like:
```
package main

func main() {
    log.Begin()
    
    log.End()
}
```

The logger you create will be represents by a type:
```
type Logger struct {
    //@TODO: you will need to figure out what goes here.
}
```

This logger will provide methods to output text BUT you will write it in a way that you have the ability to turn on and off the outputted text, and decide where you want the output to go.

The first method your logger will have is:
```
func (receiver Logger) Log(a ...interface{}) {
    //@TODO:  you will need to figure out what goes here.
}
```
The other two methods your logger will have are:
```
func (receiver Logger) Begin(a ...interface{}) {
    //@TODO:  you will need to figure out what goes here.
}
```

```
func (receiver Logger) End(a ...interface{}) {
    //@TODO:  you will need to figure out what goes here.
}
```

These other two methods should use the `Log()` method (you created before) to do their outputting.


Hints:
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln) — `fmt.Fprintln()` is similar to `fmt.Println()` except `fmt.Fprintln()` lets you tell it where to send the output.
* [os.Stdout](https://golang.org/pkg/os/#Stdout) — `os.Stdout` is where `fmt.Printf()` & `fmt.Println()` send their output.
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)

### 3.2. Hello {NAME} with logging

Copy your previous _Hello {NAME}_ program, but make it also log the name.

For example, if `name == "Joe"`, then it out log:
> The name was "Joe"

Alternatively, for example, if `name == "Fred"`, then it out log:
> The name was "Fred"

Etc.

So, because you are also calling the `.Begin()` & `End()` functions, then your full output will be something like:
```
BEGIN
The name was "Joe"
END
```

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

### 3.3. Repository "go-log"

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

### 3.4. Pacakge "log"

Put your logger code into the `go-log` repository you previously created.

The name of your package will be `log`. I.e.,:—
```go
package log
```

You might have noticed that the repository is called `go-log`, but the package is named `log`. That is on purpose. The convention in the Go community is to name things this way.

### 3.5. Unit Testing

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
```
func TestPunch(t *testing.T) {
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

### 3.6. import "go-log"

Write a program that uses your `"log"` package.

At the beginning of the program log:
> BEGIN

At the end of the program log:
> END

### 3.7. Verbose

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

### 3.8. Prefix

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

### 3.9. Func Name

Modify the logger you created so that your `Log()` and `Logf()` functions prefix their output with the name of the function they are called in.

So, for example, this program:
```go
package main

// ...

func main() {
	log.Log("Hello world!")
}
```
Would output something similar to:
```
main: BEGIN
main: END
```

Hints:
* [runtime.Caller()](https://golang.org/pkg/runtime/#Caller)
* [runtime.FuncForPC()](https://golang.org/pkg/runtime/#FuncForPC)
* [runetime.Func.Name()](https://golang.org/pkg/runtime/#Func.Name)


### 3.10. Timer

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

To do this we are going to are going to radically change how `.Begin()` and `.End()` work.

We need to make it so calling `.Begin()` №1 still outputs what it did before but now №2 returns a new logger. I.e.,:—
```go
sublogger := log.Begin()
```

And then when we call `.End()` it is on this new logger. I.e.,:—
```go
sublogger.End()
```

So, a more full example might be:
```go
locallogger := log.Begin()

locallogger.Logf("The name was %q", name)

locallogger.End()
```

**Make this change, and then create a program that uses them.**

Hints:
* [time.Time](https://golang.org/pkg/time/#Time)
* [time.Now()](https://golang.org/pkg/time/#Now)

### 3.11. Leveled Logger

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
	
	Begin(a ...interface{}) Logger
	
	End(a ...interface{})
	
	Level(uint8) Logger
}
```

And make it so that your logger has a concept of a “level”.

* level 0 — _nothing_ is outputted
* level 1 — only **alert**, and **error** are outputted
* level 2 — everything from level 1 is outputted, plus **highlight** is also outputted
* level 3 — everything from level 2 is outputted, plus **warn** is also outputted
* level 4 — everything from level 3 is outputted, plus **inform** is also outputted
* level 5 — everything from level 4 is outputted, plus **log** is also outputted
* level 6 — everything from level 5 if outputted, plus **trace** is also outputted

-----

[RETURN](../../README.md)