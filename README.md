[![GoDoc](https://godoc.org/github.com/alexflint/go-memdump?status.svg)](https://godoc.org/github.com/alexflint/go-memdump)
[![Build Status](https://travis-ci.org/alexflint/go-memdump.svg?branch=master)](https://travis-ci.org/alexflint/go-memdump)
[![Coverage Status](https://coveralls.io/repos/alexflint/go-memdump/badge.svg?branch=master&service=github)](https://coveralls.io/github/alexflint/go-memdump?branch=master)
[![Report Card](https://goreportcard.com/badge/github.com/alexflint/go-memdump)](https://goreportcard.com/badge/github.com/alexflint/go-memdump)

## Very fast serialization for Go

This package provides a fast but unsafe way to load amounts of data into Go structs. `go-memdump` can load multiple gigabytes per second, even when the data contains large numbers of small structs with many pointers and slices. However, the price you pay for decoding performance is:
- you cannot load into structs that contain maps or interfaces
- your data is not portable across architectures
- encoding is not particularly fast

Memdump was designed for use in a caching layer, where the data was encoded and decoded by the same machine, and where decoding performance mattered more than encoding performance.

## Quick start

```shell
go get github.com/alexflint/go-memdump
```

Write data to a file:

```go
type data struct {
	Foo string
	Bar int
}
mydata := data{Foo: "abc", Bar: 123}
f, _ := os.Create("/tmp/data.memdump")
memdump.Encode(f, &args)
```

Load data from a file:

```go
var mydata data
f, _ := os.Open("/tmp/data.memdump")
memdump.Decode(f, &mydata)
```

### Benchmarks

Coming soon