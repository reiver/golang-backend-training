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
* [2. Logging](#2-logging)
* [3. Web Server](#3-web-server)
* [4. Database](#4-database)
* [5. Database & Go](#5-database--go)

-----

## 0. PREFACE

Do NOT skip any sections.

Do all sections. And do all the sections in the order that they appear in this guide.

Also, the point of this is that you show your work to someone more experienced with the Go programming language, so that they can give you feedback, tips, etc, so you can learn Go faster.

## 1. Outputting

### 1.1. Create a Go program that outputs text

Create a Go program that outputs the text:
> Hello world!

Hints:
* [fmt.Println()](https://golang.org/pkg/fmt/#Println)
* [installing Go](https://golang.org/doc/install)
* [getting started with Go](https://golang.org/doc/tutorial/getting-started)

### 1.2. Hello {NAME}

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

## 2. Logging

### 2.1. Create a simple logger

Create a logger. The logger will provide functions or methods to output text BUT you will have the ability to turn on and off the outputted text, and decide where you want the output to go.

Then write a program that uses that logger, and:—

At the beginning of the program it logs:
> BEGIN

At the end of the program it logs:
> END

You should create a type to represent this logger called:
```
type Logger struct {
    //@TODO: you will need to figure out what goes here.
}
```

And the logger should have these three methods.

The first method should be:
```
func (receiver Logger) Log(a ...interface{}) {
    //@TODO:  you will need to figure out what goes here.
}
```

The other two methods are:
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

And these other two methods should use the `Log()` method you created before.

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf) — `fmt.Fprintf()` is similar to `fmt.Printf()` except `fmt.Fprintf()` lets you tell it where to send the output.
* [fmt.Fprintln()](https://golang.org/pkg/fmt/#Fprintln) — `fmt.Fprintln()` is similar to `fmt.Println()` except `fmt.Fprintln()` lets you tell it where to send the output.
* [os.Stdout](https://golang.org/pkg/os/#Stdout) — `os.Stdout` is where `fmt.Printf()` & `fmt.Println()` send their output.
* [ioutil.Discard](https://golang.org/pkg/io/ioutil/#Discard)
* [io.Writer](https://golang.org/pkg/io/#Writer)

### 2.2. Hello {NAME} with logging

Copy your previous _Hello {NAME}_ program, but make it also log the name.

For example, if `name == "Joe"`, then it out log:
> The name was "Joe"

Alternatively, for example, if `name == "Fred"`, then it out log:
> The name was "Fred"

Etc.

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)

### 2.3. Repository "go-log"

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

### 2.4. Pacakge "log"

Put your logger code into the `go-log` repository you previously created.

### 2.5. import "go-log"

Write a program that uses your `"log"` package.

At the beginning of the program log:
> BEGIN

At the end of the program log:
> END

## 3. WEB SERVER

### 3.1. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Also include logging.

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

### 3.2. Web Hello {NAME}

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

### 3.3. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

### 3.4. Web Hello {NAME} with JSON

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

### 3.5. Web Addition

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

## 4. Database

### 4.1. Install the Postgres Database Server

### 4.2. Create a Database

Use the Postgres command line tool `psql` to create a new database.

### 4.3. Create a Table

Use the Postgres command line tool `psql` to create a new table (in the database you previously created).

### 4.4. INSERT

Use the Postgres command line tool `psql` to INSERT some new values (into the new table you created in the new database you previously created).

## 5. Database & Go

### 5.1. Browse

Write a Go program that connects to the database server you previously installed and gets and outputs all the data your from the table you previously created.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

### 5.2. Read

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

### 5.3. Create

Write a Go program that connects to the database server you previously installed and creates a single row from the table you previously created.

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

### 5.4. Update

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

### 5.5. Delete

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
