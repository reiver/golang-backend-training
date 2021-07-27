# 6. JSON ([Golang Backend Training](../../README.md))

## 6.1. Output JSON

Make the Web server you wrote in Go output the JSON:
```json
{
    "msg":"Hello world!"
}
```

Also include logging.

Hints:
* [import "encoding/json"](https://golang.org/pkg/encoding/json/)

## 6.2. Web Hello {NAME} with JSON

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

## 6.3. Web Addition

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

-----

[⏮](../web_serving/README.md) [⏭️](../simple_json/README.md)
