# Golang Backend Training
by [Charles Iliya Krempeaux](http://changelog.ca/)

-----

This is a guide to help train someone to do **backend development** using the Go programming language.

**This is NOT a tutorial. This is a guide that directs someone to learn specific things.**

The whole point of this guide is that _you_ go and learn what you need to learn to be able to complete each assignment in this guide.

If you can accomplish all these tasks then you will have _a lot_ of the skills necessary to do **backend development** using the Go programming language.

This guide gives you hints. And you should spend a bit of time trying to figure out stuff yourself. **BUT DON'T SPEND TOO MUCH TIME BEING STUCK. ASK FOR HELP IF YOU GET STUCK!**

-----

## PREFACE

Do NOT skip any sections.

Do NOT skip any sections!

Do NOT skip any sections!!

**Do _all_ the sections.**

Even if they seem easy to you — still, do _all_ the sections! The point of this guide is _not_ to challenge you; the point of this guide is to get you familiar with certain parts of Go, and to correct any mistakes or misunderstandings you might have early on.

**And do all the sections in the order that they appear in this guide.**

A particular section can depend on the knowledge gained in previous sections. You need to 

The point of you going through this guide is that **you show your work to someone more experienced with the Go programming language, so that they can give you feedback, tips, etc, so you can learn Go faster**.

## TABLE OF CONTENTS

* [1. Outputting](outputting/README.md) ⟸ START HERE
* [2. Flagging](chapters/flagging/README.md)
* [3. Logging](chapters/logging/README.md)
* [4. Web Serving](chapters/web_serving/README.md)
* [5. JSON](chapters/json/README.md)
* [6. Simple JSON](chapters/simple_json/README.md)
* [7. Database](chapters/database/README.md)
* [8. Database & Go](chapters/database_and_go/README.md)
* [9. Money](chapters/money/README.md)
* [10. Option Types](#10-option-types)

-----




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

