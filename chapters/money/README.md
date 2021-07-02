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

-----

[RETURN](../../README.md)
