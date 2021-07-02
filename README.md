# Golang Backend Training
by [Charles Iliya Krempeaux](http://changelog.ca/)

-----

This is a guide to help train someone to do **backend development** using the Go programming language.

**This is NOT a tutorial. This is a guide that directs someone to learn specific things.**

The whole point of this guide is that _you_ go and learn what you need to learn to be able to complete each assignment in this guide.

If you can accomplish all these tasks, you will have _a lot_ of the skills necessary to do **backend development** using the Go programming language.

This guide gives you hints. And you should spend a bit of time trying to figure out stuff yourself. **BUT DON'T SPEND TOO MUCH TIME BEING STUCK. ASK FOR HELP IF YOU GET STUCK!**

-----

## PREFACE

Do NOT skip any sections.

Do NOT skip any sections!

Do NOT skip any sections!!

**Do _all_ the sections.**

Even if they seem easy to you — still, do _all_ the sections! The point of this guide is _not_ to challenge you; the point of this guide is to get you familiar with certain parts of Go, and to correct any mistakes or misunderstandings you might have early on.

**And do all the sections in the order that they appear in this guide.**

The point of you going through this guide is that **you show your work to someone more experienced with the Go programming language, so that they can give you feedback, tips, etc, so you can learn Go faster**.

## TABLE OF CONTENTS

* [1. Outputting](outputting/README.md)
* [2. Flagging](chapters/flagging/README.md)
* [3. Logging](chapters/logging/README.md)
* [4. Web Server](#4-web-server)
* [5. JSON](#5-json)
* [6. Simple JSON](#6-simple-json)
* [7. Database](#7-database)
* [8. Database & Go](#8-database--go)
* [9. Money](#9-money)
* [10. Option Types](#10-option-types)

-----




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

## 5. JSON

### 5.1. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

### 5.2. Web Hello {NAME} with JSON

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

### 5.3. Web Addition

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

## 6. Simple JSON

### 6.1. Simple JSON

Using the built-in `"encoding/json"`package to return an HTTP response whose payload is JSON can be quite verbose, with a lot of biolerplate looking code.

To make the _developer user experience_ better we are going to look the `simplehttp` package:

https://github.com/reiver/go-simplehttp

With this, instead of writing:
```go

import "encoding/json"

// ...

func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	w.Header().Set("Content-Type", "application/json")
	w.WriteHeader(http.StatusNotFound)
	err := json.NewEncoder(w).Encode(struct{
		StatusCode int64  `json:"status_code"`
		StatusName string `json:"status_name"`
	}{
		StatusCode: http.StatusNotFound,
		StatusName: "Not Found",
	})
	if nil != err {
		// ...
	}
}


```
We can write:
```go

import "github.com/reiver/go-simplehttp"

// ...

simplejson, err := simplehttp.Load("json")

// ...

func ServeHTTP(w http.ResponseWriter, r *http.Request) {

	// ...

	simplejson.NotFound(w)
}
```

Re-write that API end point that accepts two numbers, adds then, and outputs the result, so that it uses the `simplehttp` package to return the result. I.e.,:

`/addition?x=3&y=2`
```
{
    "result":"5",
}
```

Hints:
* [strconv.ParseInt()](https://golang.org/pkg/strconv/#ParseInt)
* [strconv.ParseUint()](https://golang.org/pkg/strconv/#ParseUint)
* [import "github.com/reiver/go-simplehttp"](https://pkg.go.dev/github.com/reiver/go-simplehttp)


## 7. Database

### 7.1. Install the Postgres Database Server

### 7.2. Create a Database

Use the Postgres command line tool `psql` to create a new database.

### 7.3. Create a Table

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

### 7.4. INSERT

Use the Postgres command line tool `psql` to INSERT some new values (into the new table you created in the new database you previously created).

## 8. Database & Go

### 8.1. Browse

Write a Go program that connects to the database server you previously installed and gets and outputs all the data your from the table you previously created.

Hints:
* [import "database/sql"](https://golang.org/pkg/database/sql/)
* [import _ "github.com/lib/pq"](https://github.com/lib/pq)
* [Go "database/sql" tutorial](http://go-database-sql.org/)

### 8.2. Read

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

### 8.3. Create

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

### 8.4. Update

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

### 8.5. Delete

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

## 9. Money

### 9.1. Type

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
	fmt.Println("should be 0.1 but as you can see it isn't!")
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

// AsCents returns CAD as the number of pennies it is equivalent to.
func (receiver) AsCents() int64 {
	//@TODO
}

// CanonicalForm returns the number of dollars and cents that CAD represents.
//
// ‘cents’ is always less than for equal to 99. I.e.,:
//	cents ≤ 99
func (receiver CAD) CanonicalForm() (dollars int64, cents int64) {
	//@TODO
}

// Mul multiplies CAD by a scalar (number) and returns the result.
func (receiver CAD) Mul(scalar int64) CAD {
	//@TODO
}

// Sub subtracts two CAD and returns the result.
func (receiver CAD) Sub(other CAD) CAD {
	//@TODO
}
```

### 9.2. Unit Tests

Write unit tests to try to verify that your implementation of each of those methods & functions is correct.

### 9.3. Program

Write a program showing each of those functions in action.

### 9.4. GoStringer

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

### 9.5. Stringer

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

### 9.6. JSON Marshal

Make it so

Hints:
* [json.Marshaler](https://golang.org/pkg/encoding/json/#Marshaler)
* [json.Marshal()](https://golang.org/pkg/encoding/json/#Marshal)

### 9.7. JSON Unmarshal

Hints:
* [json.Unmarshaler](https://golang.org/pkg/encoding/json/#Unmarshaler)
* [json.Unmarshal()](https://golang.org/pkg/encoding/json/#Unmarshal)

### 9.8. Valuer

Make it so that this custom money type you are creating can be used as an input argument to these methods from Go's built-in `"database/sql" package:

* [database/sql.Conn.ExecContext()](https://golang.org/pkg/database/sql/#Conn.ExecContext)
* [database/sql.Conn.QueryContext()](https://golang.org/pkg/database/sql/#Conn.QueryContext)
* [database/sql.Conn.QueryRowContext()](https://golang.org/pkg/database/sql/#Conn.QueryRowContext)
* [database/sql.DB.Exec()](https://golang.org/pkg/database/sql/#DB.Exec)
* [database/sql.DB.ExecContext()](https://golang.org/pkg/database/sql/#DB.ExecContext)
* [database/sql.DB.Query()](https://golang.org/pkg/database/sql/#DB.Query)
* [database/sql.DB.QueryContext()](https://golang.org/pkg/database/sql/#DB.QueryContext)
* [database/sql.DB.QueryRow()](https://golang.org/pkg/database/sql/#DB.QueryRow)
* [database/sql.DB.QueryRowContext()](https://golang.org/pkg/database/sql/#DB.QueryRowContext)
* [database/sql.Stmt.Exec()](https://golang.org/pkg/database/sql/#Stmt.Exec)
* [database/sql.Stmt.ExecContext()](https://golang.org/pkg/database/sql/#Stmt.ExecContext)
* [database/sql.Stmt.Query()](https://golang.org/pkg/database/sql/#Stmt.Query)
* [database/sql.Stmt.QueryContext()](https://golang.org/pkg/database/sql/#Stmt.QueryContext)
* [database/sql.Stmt.QueryRow()](https://golang.org/pkg/database/sql/#Stmt.QueryRow)
* [database/sql.Stmt.QueryRowContext()](https://golang.org/pkg/database/sql/#Stmt.QueryRowContext)
* [database/sql.Tx.Exec()](https://golang.org/pkg/database/sql/#Tx.Exec)
* [database/sql.Tx.ExecContext()](https://golang.org/pkg/database/sql/#Tx.ExecContext)
* [database/sql.Tx.Query()](https://golang.org/pkg/database/sql/#Tx.Query)
* [database/sql.Tx.QueryContext()](https://golang.org/pkg/database/sql/#Tx.QueryContext)
* [database/sql.Tx.QueryRow()](https://golang.org/pkg/database/sql/#Tx.QueryRow)
* [database/sql.Tx.QueryRowContext()](https://golang.org/pkg/database/sql/#Tx.QueryRowContext)

I.e., so you can do things such as:
```go

var money CAD = Cents(150) // $1.50

// ...

dbconn.Exec(`INSERT INTO bankaccount (cuatomer_id, type, amount) VALUES ($1, 'credit', $2)`, id, money)
```

And then write a program demonstating this working.

Hints:
* [database/sql/driver.Valuer](https://golang.org/pkg/database/sql/driver/#Valuer)
* [database/sql.DB.Exec()](https://golang.org/pkg/database/sql/#DB.Exec)
* [database/sql.DB.Query()](https://golang.org/pkg/database/sql/#DB.Query)
* [database/sql.DB.QueryRow()](https://golang.org/pkg/database/sql/#DB.QueryRow)

### 9.9. Scanner

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

Then make it so your custom **money** type can be `.Scan()`ed into. I.e.,:
```go
var id    int64
var kind  string
var money CAD // <----

// ...
for rows.Next() {
	// ...

	//                            ↓↓↓↓↓
	err := rows.Scan(&id, &kind, &money)

	// ...
}
```

And then write a program that scans data from the database into your custom **money** type.

Hints:
* [database/sql.Scanner](https://golang.org/pkg/database/sql/#Scanner)
* [database/sql.Rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan)
* [database/sql.Row.Scan()](https://golang.org/pkg/database/sql/#Row.Scan)
* [Pointer receivers](https://tour.golang.org/methods/4)
* [Choosing a value or pointer receiver](https://tour.golang.org/methods/8)


## 10. Option Types

### 10.1. Type

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

### 10.2. GoStringer

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

### 10.3. Stringer

Hints:
* [fmt.Stringer](https://golang.org/pkg/fmt/#Stringer)

### 10.4. JSON Marshal

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

### 10.5. JSON Unmarshal

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

### 10.6. Valuer

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

### 10.7. Scanner

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

