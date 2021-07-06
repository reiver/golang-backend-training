# 11. Go Project Structure ([Golang Backend Training](../../README.md))

## 11.1. Project Structure

If you have gone through this guide, then you have likely already discovered the suggested Go project structure. The different chapters of this guide touch on different aspets of the suggested Go project layout.

But I think it is a good idea to explicitly specify it in a chapter, so the information is in one place. So here it is:

* `main.go`
  * `arg/`
  * `cfg/`
  * `lib/`
  * `srv/`

**Of course, you can have other directories & files in addition to these.**
But these are the basics that likely most your Go projects will have.

## 11.2. arg/

Before `main()` is called, things start in the `args/` diretory.

The code in the `args/` directory uses the Go built-in ["flag"](https://golang.org/pkg/flag/) package to make things happen.

This package is very simple. It just expored variables.

For example, you might have:

* arg.Value
* arg.Verbose
* arg.VeryVerbose
* arg.VeryVeryVerbose
* arg.VeryVeryVeryVerbose
* arg.VeryVeryVeryVeryVerbose
* arg.VeryVeryVeryVeryVeryVerbose

You might even have:

* arg.Colored
* arg.Query
* arg.HttpPort

It is probably going to look something like:
```go
package arg

import "flag"

var (
	Query string
)

var (
	Verbose bool
	VeryVerbose bool
	VeryVeryVerbose bool
	VeryVeryVeryVerbose bool
	VeryVeryVeryVeryVerbose bool
	VeryVeryVeryVeryVeryVerbose bool
)


func init() {
	flag.StringVar(&Query, "q", "", "search query")

	flag.BoolVar(&Verbose,                     "v",      false,                          "verbose logs outputted")
	flag.BoolVar(&VeryVerbose,                 "vv",     false,                     "very verbose logs outputted")
	flag.BoolVar(&VeryVeryVerbose,             "vvv",    false,                "very very verbose logs outputted")
	flag.BoolVar(&VeryVeryVeryVerbose,         "vvvv",   false,           "very very very verbose logs outputted")
	flag.BoolVar(&VeryVeryVeryVeryVerbose,     "vvvvv",  false,      "very very very very verbose logs outputted")
	flag.BoolVar(&VeryVeryVeryVeryVeryVerbose, "vvvvvv", false, "very very very very very verbose logs outputted")

	flag.Parse()
}
```


## 11.3. cfg/

Next `cfg/` directory contains the configuration parameters. These are just simple variables.

For example, some configuration parameters might be:

* cfg.DefaultHttpPort
* cfg.DBHost
* cfg.DBName
* cfg.DBPassword
* cfg.DBUsername

## 11.4. lib/

The `lib/` diretory contain local libraries.

For example, some local libraries might be:

* lib/formletter
* lib/model/account
* lib/model/user

## 11.5. srv/

The `srv/` directory contains services.

For example, your configured & instantiated logger is a service. You might put it at: `srv/log`

Also, for example, you configured & instantiated connection to the database is service. You might put it at: `srv/db`

Etc.

