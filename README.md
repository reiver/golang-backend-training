# Golang Backend Training

This is a guide to help train someone to do **backend development** using the Go programming language.

**This is NOT a tutorial. This is a guide that directs to learn specific things.**

The whole point of this is that you go and learn what you need to learn to be able to complete each assignment.

If you can accomplish all these tasks, you will have _a lot_ of the skills necessary to do **backend development** using the Go programming language.

This guide gives you hints. And you should spend a bit of time trying to figure out stuff yourself. **BUT DON'T SPEND TOO MUCH TIME BEING STUCK. ASK FOR HELP IF YOU GET STUCK!**

## 0. PREFACE

Do NOT skip any sections.

Do all sections. And do all the sections in the order that they appear in this guide.

Also, the point of this is that you show your work to someone more experienced with the Go programming language, so that they can give you feedback, tips, etc, so you can learn Go faster.

## 1. PROGRAMS

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

### 1.3. Create a simple logger

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

### 1.4. Hello {NAME} with logging

Copy your previous _Hello {NAME}_ program, but make it also log the name.

For example, if `name == "Joe"`, then it out log:
> The name was "Joe"

Alternatively, for example, if `name == "Fred"`, then it out log:
> The name was "Fred"

Etc.

Hints:
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)

## 2. WEB SERVER

### 2.1. Create a Web server

Create a Web server in Go, where the Web server outputs:
> Hello world

Also include logging.

Hints:
* [import "net/http"](https://golang.org/pkg/net/http/)

### 2.2. Web Hello {NAME}

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

### 2.3. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

### 2.4. Web Hello {NAME} with JSON

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

### 2.5. Web Addition

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

## 3. Database

### 3.1. Install the Postgres Database Server

### 3.2. Create a Database

Use the Postgres command line tool `psql` to create a new database.

### 3.3. Create a Table

Use the Postgres command line tool `psql` to create a new table (in the database you previously created).

### 3.4. INSERT

Use the Postgres command line tool `psql` to INSERT some new values (into the new table you created in the new database you previously created).

## 4. Database & Go

### 4.1. Browse

Write a Go program that connects to the database server you previously installed and gets and outputs all the data your from the table you previously created.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)

### 4.2. Read

Write a Go program that connects to the database server you previously installed and gets a single row from the table you previously created.

Use a variable to specify the ID of the row you want to get. For example:
```Go
var id int64 = 123
```

Also include logging.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)

### 4.3. Create

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

### 4.4. Update

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

### 4.5. Delete

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
