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

The code that deals the flags should be in `flags.go`

The code that deals with the outputting should be in `main.go`

Once you have done that, do a `go build` and make sure everything still works.

## 2.4. Flags Sub Directory

To help make your code even more manageable, let's put all the flag code into a sub-directory named: `flags/`

So that your code will look something like:

* main.go
* flags/
  * flags.go

You will need to `import` this sub-directory from `main.go` to use it.

The code that deals the flags should be in `flags/flags.go`

The code that deals with the outputting should be in `main.go`

Once you have done that, do a `go build` and make sure everything still works.

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

-----

[RETURN](../../README.md)
