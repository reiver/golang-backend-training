# 2. Flagging ([Golang Backend Training](../../README.md))

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


## 2.3. Arg File

To help make your code more manageable, let's put all the flag code into a separate file named: `arg.go`

So that your code base will look something like:
* main.go
* arg.go

The code that deals the flags should be in `arg.go`

The code that deals with the outputting should be in `main.go`

Once you have done that, do a `go build` and make sure everything still works.

## 2.4. Arg Sub Directory

To help make your code even more manageable, let's put all the flag code into a sub-directory named: `arg/`

So that your code will look something like:

* main.go
* arg/
  * arg.go

You will need to `import` this sub-directory from `main.go` to use it.

The code that deals the flags should be in `arg/arg.go`

The code that deals with the outputting should be in `main.go`

Once you have done that, do a `go build` and make sure everything still works.

## 2.5. init()

To make the flags get their values you have to run [flag.Parse()](https://golang.org/pkg/flag/#Parse).

It would be nice if our `arg/` sub-directory could do this all by itself.

We can run initialization code from a special magical `init()` function. Create an init() function in the `arg/` sub-directory:
```go
func init() {
	//@TODO
}
```

And then run [flag.Parse()](https://golang.org/pkg/flag/#Parse) from it, to make the flags get their values.

Hints:
* [Effective Go: The init function](https://golang.org/doc/effective_go#init)

## 2.6. flag.Var

Package `flag` comes with built-in support for a number of types:

* `bool`
* `float64`
* `int`
* `int64`
* `string`
* `uint`
* `uint64`

If you want to load the value of a command line flag into a custom type, then the custom would need to implement the `flag.Value` inteface:
```golang
type Value interface {
	String() string
	Set(string) error
}
```

Create a custom type that (also) implements the `flag.Value` interface, and write a program that loads a value into it from a command line flag using the `flag.Value` interface.


Hints:
* [flag.Value](https://pkg.go.dev/flag#Value)


-----

[⏮](../outputting/README.md) [⏭️](../interfaces/README.md)
