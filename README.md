# Golang Backend Training
by [Charles Iliya Krempeaux](http://changelog.ca/)

-----

This is a guide to help train someone to do **backend development** using the Go programming language.

**This is NOT a tutorial. This is a guide that directs someone to learn specific things.**

The whole point of this guide is that _you_ go and learn what you need to learn to be able to complete each assignment in this guide.

If you can accomplish all these tasks, you will have _a lot_ of the skills necessary to do **backend development** using the Go programming language.

This guide gives you hints. And you should spend a bit of time trying to figure out stuff yourself. **BUT DON'T SPEND TOO MUCH TIME BEING STUCK. ASK FOR HELP IF YOU GET STUCK!**

## TABLE OF CONTENTS

* [0. Preface](#0-preface)
* [1. Outputting](#1-outputting)
* [2. Flagging](#2-flagging)
* [3. Logging](#3-logging)
* [4. Web Server](#4-web-server)
* [5. Database](#5-database)
* [6. Database & Go](#6-database--go)
* [7. Money](#7-money)
* [8. Option Types](#8-option-types)

-----

## 0. PREFACE

Do NOT skip any sections.

Do NOT skip any sections!

Do NOT skip any sections!!

**Do _all_ the sections.**

Even if they seem easy to you — still, do _all_ the sections! The point of this guide is _not_ to challenge you; the point of this guide is to get you familiar with certain parts of Go, and to correct any mistakes or misunderstandings you might have early on.

**And do all the sections in the order that they appear in this guide.**

The point of you going through this guide is that **you show your work to someone more experienced with the Go programming language, so that they can give you feedback, tips, etc, so you can learn Go faster**.

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

## 2. Flagging

## 2.1. Flag Hello {NAME}

Modify your previous **Hello {NAME}** program so that the name comes from a command line flag.

So, for example, if your program is name `myprogram`, and it is run with:
```
myprogram --name=Joe
```
Then it outputs:
```
Hello Joe!
```

Etc.

Hints:
* [import "flag"](https://golang.org/pkg/flag/)
* [flag.StringVar()](https://golang.org/pkg/flag/#StringVar)
* [flag.Parse()](https://golang.org/pkg/flag/#Parse)

## 2.2. Shhh

Modify your previous program to add  `--shhh` flag. The `--shhh` will make it so nothing will output.

So, for example, if your program is name `myprogram`, and it is run with:
```
myprogram --name=Joe
```
Then it outputs:
```
Hello Joe!
```
And, again for example, if again your program is name `myprogram`, and this time it is run with:
```
myprogram --name=Joe --shhh
```
Then it would output nothing.

Hints:
* [import "flag"](https://golang.org/pkg/flag/)
* [flag.BoolVar()](https://golang.org/pkg/flag/#BoolVar)
* [flag.Parse()](https://golang.org/pkg/flag/#Parse)


## 2.3. Flags File

To help make your code more manageable, let's put all the flag code into a separate file named: `flags.go`

So that your code base will look something like:
* main.go
* flags.go

Once you have done that, do a `go build` and make sure everything still works.

## 2.4. Flags Sub Directory

To help make your code even more manageable, let's put all the flag code into a sub-directory named: `flags/`

So that your code will look something like:

* main.go
* flags/
  * flags.go

You will need to `import` this sub-directory from `main.go` to use it.

## 2.5. init()

To make the flags get their values you have to run [flag.Parse()](https://golang.org/pkg/flag/#Parse).

It would be nice if our `flags/` sub-directory could do this all by itself.

We can run initialization code from a special magical `init()` function. Create an init() function in the `flags/` sub-directory:
```go
func init() {
	//@TODO
}
```

And then run [flag.Parse()](https://golang.org/pkg/flag/#Parse) from it, to make the flags get their values.

Hints:
* [Effective Go: The init function](https://golang.org/doc/effective_go#init)

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

We need to make it so calling `.Begin()` №1 still outputs what it did because but now №2 returns a new logger. I.e.,:—
```go
sublogger := log.Begin()
```

And then when we call `.End()` it is on this new logger. I.e.,:—
```go
sublogger.End()
```

**Make this change, and then create a program that uses them.**

Hints:
* [time.Time](https://golang.org/pkg/time/#Time)
* [time.Now()](https://golang.org/pkg/time/#Now)

### 3.11. Leveled Logger

Sometimes it is useful to have a logger that can categorize its logs, and turn on and off the different categories of logs.

Change your logged to have these levels:
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
	Beginf(format string, a ...interface{}) Logger
	
	End(a ...interface{})
	Endf(format string, a ...interface{})
}
```

## 4. WEB SERVER

### 4.1. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Also include logging.

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

### 4.2. Web Hello {NAME}

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

Hint:
* [fmt.Fprintf](https://golang.org/pkg/fmt/#Fprintf)
* [http.Handler](https://golang.org/pkg/net/http/#Handler)
* [http.ResponseWriter](https://golang.org/pkg/net/http/#ResponseWriter)

### 4.3. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

### 4.4. Web Hello {NAME} with JSON

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

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

### 4.5. Web Addition

Create an API end point that accepts two numbers, adds then, and outputs the result.

For example:

`/addition?x=3&y=2`
```
{
    "result":"5",
}
```

Hints:
* [strconv.ParseInt()](https://golang.org/pkg/strconv/#ParseInt)
* [strconv.ParseUint()](https://golang.org/pkg/strconv/#ParseUint)
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

## 5. Database

### 5.1. Install the Postgres Database Server

### 5.2. Create a Database

Use the Postgres command line tool `psql` to create a new database.

### 5.3. Create a Table

Use the Postgres command line tool `psql` to create a new table (in the database you previously created).

Your table should include a field that is its _primary key_:
```
id BIGSERIAL PRIMARY KEY,
```

And it should include a field named `when_created`:
```sql
when_created TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT now(),
```

Of course, you should have other fields besides this one. Make up some type of table. And include fields that make sense for your made up table.

### 5.4. INSERT

Use the Postgres command line tool `psql` to INSERT some new values (into the new table you created in the new database you previously created).

## 6. Database & Go

### 6.1. Browse

Write a Go program that connects to the database server you previously installed and gets and outputs all the data your from the table you previously created.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

### 6.2. Read

Write a Go program that connects to the database server you previously installed and gets a single row from the table you previously created.

Use a variable to specify the ID of the row you want to get. For example:
```Go
var id int64 = 123
```

Also include logging.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

### 6.3. Create

Write a Go program that connects to the database server you previously installed and creates a single row from the table you previously created.

**Your program needs to also output the PRIMARY KEY of the row you just created.**

(Note that there is a trick to getting the PRIMARY KEY of the INSERTed row using Postgres in Golang, as the `"pq"` package does NOT support `LastInsertId()`. The [pq Queries](https://pkg.go.dev/github.com/lib/pq#hdr-Queries) hint talks about how to get it using the "RETURNING id" technique.)

Use a variable to specify the ID of the row you want to get. For example:
```Go
var id int64 = 123
```

And use other variables for the fields for the row that you are creating.

Also include logging.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)
* [pq Queries](https://pkg.go.dev/github.com/lib/pq#hdr-Queries)

### 6.4. Update

Write a Go program that connects to the database server you previously installed and updates a single row from the table you previously created.

Use a variable to specify the ID of the row you want to get. For example:
```Go
var id int64 = 123
```

And use other variables for the fields that you update.

Also include logging.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

### 6.5. Delete

Write a Go program that connects to the database server you previously installed and delete a single row from the table you previously created.

Use a variable to specify the ID of the row you want to get. For example:
```Go
var id int64 = 123
```

And use other variables for the fields for the row that you are creating.

Also include logging.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

## 7. Money

### 7.1. Type

Go does NOT have any built-in types to safely represent money. So we are going to create a custom type to represent money in Go.

**And we are _not_ going to make the mistake of storing money using float64 or float32.** For example, if you want to see an example of the problem with using float to represent money, run the follow code:
```go
package main

import (
	"fmt"
)

func main() {
	var a float64 = 0.01
	var b float64 = 0.09
	
	var result float64 = a + b

	fmt.Printf("result = %#v \n", result)	
	fmt.Println("should be: 0.1")
}
```

(Many many people get really really really get pissed off if you don't get money calcuations perfect. So we are going to make it so our money calculations are perfect.)

So we are going to create our own money type, and we are going to do it right.

We are going to create a type to represent Canadian Dollars (CAD):
```go
type CAD struct {
    //@TODO
}
```

To make it so we have exact values and perfect math, we are going to (secretly) store the dollar amount as cents. I.e.,:
```go
type CAD struct {
    cents int64
}
```

(Note that we are using `int64` rather than `uint64`. In doing that we can represent **negative** money values too. Such as: -$3.50. Which is good.)

Your first task is to implement these functions:
```go
// Cents returns a CAD that represents ‘n’ cents.
//
// For example, if one was to call:
//
//	cad := Cents(105)
//
// Then ‘cad’ would be: $1.05
func Cents(n int64) CAD {
	//@TODO
}

// ParseCAD parses the string ‘s’ and return the equivalent CAD.
//
// If ‘s’ does not contain a money amount, then ParseCAD returns an error.
//
// Some example valid strings include:
//
// • -$1234.56
// • $-1234.56
// • -$1,234.56
// • $-1,234.56
// • CAD -$1234.56
// • CAD $-1234.56
// • CAD-$1,234.56
// • CAD$-1,234.56
// • $1234.56
// • $1,234.56
// • CAD $1234.56
// • CAD $1,234.56
// • CAD$1234.56
// • CAD$1,234.56
// • $0.09
// • $.09
// • -$0.09
// • -$.09
// • $-0.09
// • $-.09
// • CAD $0.09
// • CAD $.09
// • CAD -$0.09
// • CAD -$.09
// • CAD $-0.09
// • CAD $-.09
// • CAD$0.09
// • CAD$.09
// • CAD-$0.09
// • CAD-$.09
// • CAD$-0.09
// • CAD$-.09
// • 9¢
// • -9¢
// • 123456¢
// • -123456¢
// 
func ParseCAD(s string) (CAD, error) {
	//@TODO
}

// Abs returns the absolute value.
func (receiver CAD) Abs() CAD {
 	//@TODO
}

// Add adds two CAD and returns the result.
func (receiver CAD) Add(other CAD) CAD {
	//@TODO
}

// Count return the number of dollars and cents that CAD represents.
//
// ‘cents’ is always less than for equal to 99. I.e.,:
//	cents ≤ 99
func (receiver CAD) Count() (dollars int64, cents int64) {
	//@TODO
}

// Mul multiplies CAD by a scalar (number) and returns the result.
func (receiver CAD) Mul(scalar int64) CAD {
	//@TODO
}

// NumCents returns CAD as the number of pennies it is equivalent to.
func (receiver) CountCents() int64 {
	//@TODO
}

// Sub subtracts two CAD and returns the result.
func (receiver CAD) Sub(other CAD) CAD {
	//@TODO
}
```

### 7.2. Unit Tests

Write unit tests to try to verify that your implementation of each of those methods & functions is correct.

### 7.3. Program

Write a program showing each of those functions in action.

### 7.4. GoStringer

The Go [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf), [fmt.Printf()](https://golang.org/pkg/fmt/#Printf), and [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf) functions have a **flag** that lets you see the **Go-syntax representation of the value**.

To do this we use the following flag:
```
%#v
```

For example:
```
var name string = "Joe Blow"

fmt.Printf("name = %#v", name)
```
This would output:
```
name = "Rex"
```

And also, for example:
```
type Dog struct {
    Name string
}

var myDog Dog

myDog.Name = "Rex"

fmt.Printf("myDog = %#v", myDog)
```
This would output something like:
```
myDog = main.Dog{Name:"Rex"}
```

If we were to use `%#v` on our **money type** then it would try to display the struct. Which isn't ideal. We can do better than this!

Make it so that this:
```
var money CAD
var err error

money, err = ParseCAD("$1.23)

fmt.Printf("money = %#v" , opt)
```
Outputs:
```
opt = Cents(123)
```

Etc.

And write units tests for this too.

And write an **example** program that shows this in action.

Hints:
* [fmt.GoStringer](https://golang.org/pkg/fmt/#GoStringer)
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)
* [fmt.Printf()](https://golang.org/pkg/fmt/#Printf)
* [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf)

### 7.5. Stringer

Make it so this:
```go
money, err := ParseCAD("$1.23")

fmt.Println("money:", money)
```
Outputs:
```
money: $1.23
```

And write units tests for this too.

And write an **example** program that shows this in action.

Hints:
* [fmt.Stringer](https://golang.org/pkg/fmt/#Stringer)
* [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf)

### 7.6. JSON Marshal

Hints:
* [json.Marshaler](https://golang.org/pkg/encoding/json/#Marshaler)
* [json.Marshal()](https://golang.org/pkg/encoding/json/#Marshal)

### 7.7. JSON Unmarshal

Hints:
* [json.Unmarshaler](https://golang.org/pkg/encoding/json/#Unmarshaler)
* [json.Unmarshal()](https://golang.org/pkg/encoding/json/#Unmarshal)

### 7.8. Valuer

Hints:
* [database/sql/driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer)
* [database/sql.DB.Exec()](https://golang.org/pkg/database/sql/#DB.Exec)
* [database/sql.DB.Query()](https://golang.org/pkg/database/sql/#DB.Query)
* [database/sql.DB.QueryRow()](https://golang.org/pkg/database/sql/#DB.QueryRow)

### 7.9. Scaner

Hints:
* [database/sql.Scanner](https://golang.org/pkg/database/sql/#Scanner)
* [database/sql.Rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan)
* [database/sql.Row.Scan()](https://golang.org/pkg/database/sql/#Row.Scan)

## 8. Option Types

### 8.1. Type

You can think of an **option types** as a _container_ that either has _nothing_ in it, or it can have _something_ in it.

Let's make an **option type** for `int64`. So that this _int64 option type_ will either have nothing in it, or will have an int64 value in it.

Make this code work:

```
type Int64Option struct {
    //@TODO
}

// Nothing returns an option with nothing in it.
func Nothing() Int64Option {
    //@TODO
}

// Something returns an option with ‘ value’ in it.
func Something(value int64) Int64Option {
    //@TODO
}

// Return returns the value it store if there is something in it, else it return an error.
func (receiver Int64Option) Return() (int64, error) {
    //@TODO
}
```

### 8.2. GoStringer

The Go [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf), [fmt.Printf()](https://golang.org/pkg/fmt/#Printf), and [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf) functions have a **flag** that lets you see the **Go-syntax representation of the value**.

To do this we use the following flag:
```
%#v
```

For example:
```
var name string = "Joe Blow"

fmt.Printf("name = %#v", name)
```
This would output:
```
name = "Rex"
```


And also, for example:
```
type Dog struct {
    Name string
}

var myDog Dog

myDog.Name = "Rex"

fmt.Printf("myDog = %#v", myDog)
```
This would output something like:
```
myDog = main.Dog{Name:"Rex"}
```

If we were to use `%#v` on your **option type** then it would try to display the struct.

Make it so that this:
```
var opt Int64Option = Nothing()

fmt.Printf("opt = %#v" , opt)
```
Outputs:
```
opt = Nothing()
```

And:
```
var opt Int64Option = Something(42)

fmt.Printf("opt = %#v" , opt)
```
Outputs:
```
opt = Something(42)
```

Etc.


Hints:
* [fmt.GoStringer](https://golang.org/pkg/fmt/#GoStringer)
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)
* [fmt.Printf()](https://golang.org/pkg/fmt/#Printf)
* [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf)

### 8.3. Stringer

Hints:
* [fmt.Stringer](https://golang.org/pkg/fmt/#Stringer)

### 8.4. JSON Marshal

Make it so your **option type** can be represented as JSON as:—

For nothing:
```
"nothing()"
```

For something:
```
"something(5)"
```

Then write a program that demonstrates this being used.

Hints:
* [json.Marshaler](https://golang.org/pkg/encoding/json/#Marshaler)
* [json.Marshal()](https://golang.org/pkg/encoding/json/#Marshal)

### 8.5. JSON Unmarshal

Make it so your **option type** can be parse from a JSON representation of:—

For nothing:
```
"nothing()"
```

For something:
```
"something(5)"
```

Then write a program that demonstrates this being used.

Hints:
* [json.Unmarshaler](https://golang.org/pkg/encoding/json/#Unmarshaler)
* [json.Unmarshal()](https://golang.org/pkg/encoding/json/#Unmarshal)

### 8.6. Valuer

If you are putting data into a database in Go, then you will probably either use [database/sql.DB.Exec()](https://golang.org/pkg/database/sql/#DB.Exec) or [database/sql.DB.QueryRow()](https://golang.org/pkg/database/sql/#DB.QueryRow) (or something similar to them).

By default, these  methods will only understand basic types.

**So how do you put your own custom type into the database?**

That is what you need to figure out.

Then make it so your **option type** can put into a database.

And then write a program that INSERTs your **option type** INTO the database.

Hints:
* [database/sql/driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer)
* [database/sql.DB.Exec()](https://golang.org/pkg/database/sql/#DB.Exec)
* [database/sql.DB.Query()](https://golang.org/pkg/database/sql/#DB.Query)
* [database/sql.DB.QueryRow()](https://golang.org/pkg/database/sql/#DB.QueryRow)

### 8.7. Scanner

If you are getting data from a database in Go, then you will probably either use [database/sql.Rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) or [database/sql.Row.Scan()](https://golang.org/pkg/database/sql/#Row.Scan) (or something similar to them).

By default, these `.Scan()` methods will scan into (a pointer to):

* string
* []byte
* int
* int8
* int16
* int32
* int64
* uint
* uint8
* uint16
* uint32
* uint64
* bool
* float32
* float64
* interface{}
* sql.RawBytes

**But how do you `.Scan()` into your own custom type?**

That is what you need to figure out.

Then make it so your **option type** can be `.Scan()`ed into.

And then write a program that scans data from the database into your **option type**.

Hints:
* [database/sql.Scanner](https://golang.org/pkg/database/sql/#Scanner)
* [database/sql.Rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan)
* [database/sql.Row.Scan()](https://golang.org/pkg/database/sql/#Row.Scan)

