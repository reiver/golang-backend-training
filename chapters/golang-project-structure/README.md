# 11. Go Project Structure ([Golang Backend Training](../../README.md))

## 11.1. Project Structure

If you have gone through this guide, then you have likely already discovered the suggested Go project structure. The different chapters of this guide touch on different aspets of the suggested Go project layout.

But I think it is a good idea to explicitly specify it in a chapter, so the information is in one place. So here it is:

* `main.go`
  * `arg/` (command line arguments)
  * `cfg/` (configuration parameters)
  * `lib/` (local libraries)
  * `srv/` (services)

**Of course, you can have other directories & files in addition to these.**
But these are the basics that likely most your Go projects will have.

## 11.2. arg/

Before `main()` is called, things start in the `args/` diretory.

The code in the `args/` directory uses the Go built-in ["flag"](https://golang.org/pkg/flag/) package to make things happen.

This package is very simple. It just exports variables.

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
// file: arg/arg.go
package arg

import "flag"

var (
	Values []string
)

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
	
	Values = flag.Args()
}
```


## 11.3. cfg/

Next `cfg/` directory contains the configuration parameters. These are just simple constants.

(Although some might be variables, rather than constants, if Go doesn't permit a constant for that type.)

(Also, if a configuration parameter depends on something from the `arg/` directory, then it might be a variagble, rather than a constant, to accomodate that.)

For example, some configuration parameters might be:

* cfg.DefaultHttpPort
* cfg.DBHost
* cfg.DBName
* cfg.DBPassword
* cfg.DBUsername

It will probably look something like:


```go
// cfg/db.go
package cfg

const (
	DBHost = "db.example.com"
	DBName = "blog"
	DBPassword = "it.is.a.secret123"
	DBUsername = "blogmaster"
)
```

```go
// cfg/http.go
package cfg

const (
	DefaultHttpPort = 8080
)
```

```go
// cfg/payapi.go
package cfg

import "?????/arg"

var PayApiUrl = ""

func init() {

	switch arg.DeploymentEnvironment {
	case "DEV":
		PayApiUrl = "http://localhost:8080/v1/pay"
	case "QA":
		PayApiUrl = "https://api.qa.example.com/v1/pay"
	case "STAGING":
		PayApiUrl = "https://api.staging.example.com/v1/pay"
	case "PROD"
		PayApiUrl = "https://api.example.com/v1/pay"
	default:
		panic("Unknown Deployment Environment: "+ arg.DeploymentEnvironment)
	}
}
```

Etc.

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

For example:
```go
// srv/log/logger.go
package logsrv

import (
	"github.com/???????/go-log"

	"???????/arg"
)

var (
	Logger log.Logger
)

func init() {
	//@TODO: make the output of the logger go to os.Stdout

	switch {
	case cfg.VeryVeryVeryVeryVeryVerbose:
		Logger = Logger.Level(6)
	case cfg.VeryVeryVeryVeryVerbose:
		Logger = Logger.Level(5)
	case cfg.VeryVeryVeryVerbose:
		Logger = Logger.Level(4)
	case VeryVeryVerbose:
		Logger = Logger.Level(3)
	case VeryVerbose:
		Logger = Logger.Level(2)
	case Verbose:
		Logger = Logger.Level(1)
	default:
		Logger = Logger.Level(0)
	}
}
```
