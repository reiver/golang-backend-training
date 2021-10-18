## 10. Option Types

### 10.1. Type

You can think of an **option types** as a _container_ that either has _nothing_ in it, or it can have _something_ in it.

Let's make an **option type** for `int64`. So that this _int64 option type_ will either have nothing in it, or will have an int64 value in it.

Make this code work:

```
package int64option

type Type struct {
    //@TODO
}

// Nothing returns an option with nothing in it.
func Nothing() Type {
    //@TODO
}

// Something returns an option with ‘ value’ in it.
func Something(value int64) Type {
    //@TODO
}

// Return returns the value it store if there is something in it, else it return an error.
func (receiver Int64Option) Return() (int64, error) {
    //@TODO
}
```

**NOTE** that one of the purposes of using an option type is so you can tell if nothing has been put into it or not. Thus code like this:
```go
var data int64option.Type
```
... (where no value has explicitly been assigned to it) must have a value of `int64option.Nothing()`.

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
var opt int64option.Type = int64option.Nothing()

fmt.Printf("opt = %#v" , opt)
```
Outputs:
```
opt = int64option.Nothing()
```

And:
```
var opt int64option.Type = int64option.Something(42)

fmt.Printf("opt = %#v" , opt)
```
Outputs:
```
opt = int64option.Something(42)
```

Etc.


Hints:
* [fmt.GoStringer](https://golang.org/pkg/fmt/#GoStringer)
* [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf)
* [fmt.Printf()](https://golang.org/pkg/fmt/#Printf)
* [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf)

### 10.3. Stringer

The Go [fmt.Fprintf()](https://golang.org/pkg/fmt/#Fprintf), [fmt.Printf()](https://golang.org/pkg/fmt/#Printf), and [fmt.Sprintf()](https://golang.org/pkg/fmt/#Sprintf) functions have a **flag** that lets you see a **human-readable string representation of the value**.

To do this we use the following flag:
```
%s
```

Make it so that this:
```
var opt int64option.Type = int64option.Nothing()

fmt.Printf("opt = %s" , opt)
```
Outputs:
```
opt = ⧼nothing⧽
```

And:
```
var opt int64option.Type = int64option.Something(42)

fmt.Printf("opt = %#v" , opt)
```
Outputs:
```
opt = 42
```

Etc.


Hints:
* [fmt.Stringer](https://golang.org/pkg/fmt/#Stringer)

### 10.4. JSON Marshal

Make it so your **option type** can be represented as JSON as:—

For nothing:
```
"nothing()"
```

**And note that the JSON value for it is a string, not a number.**

For something:
```
"something(5)"
```

**And note that the JSON value for it is a string, not a number.**

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

**And note that the JSON value for it is a string, not a number.**

For something:
```
"something(5)"
```

**And note that the JSON value for it is a string, not a number.**

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

-----

[RETURN](../../README.md)
