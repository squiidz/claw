claw [![GoDoc](https://godoc.org/github.com/squiidz/claw?status.png)](http://godoc.org/github.com/squiidz/claw) [![Build Status](https://travis-ci.org/go-zoo/claw.svg?branch=master)](https://travis-ci.org/squiidz/claw)
=======

## NOTICE
The Original repo have move to https://github.com/go-zoo/claw

## What is claw ?

Claw is a Middleware chaining module, compatible with
every mux who respects the ` http.Handler ` interface. Claw allows you
to create Stack of middleware for specific tasks.

![alt tag](https://c2.staticflickr.com/4/3614/3452804064_edf131c788_z.jpg?zz=1)

## Features

- Uses Standard ` func (http.ResponseWriter, *http.Request) ` as Middleware.
- Also uses ` func(http.Handler) http.Handler ` as Middleware.
- Middleware Chaining.
- Global Middleware.
- Create Middleware Stack.
- Claw runs middleware in order: last enter first to run
- Compatible with every mux that implements ` http.Handler ` interface.

[ `squiidz/claw/mw` content a simple logger and recovery middleware ]

## Example
```go
package main

import "github.com/squiidz/claw"

func main() {
	// Create a new Claw instance, and set some Global Middleware.
	c := claw.New(GlobalMiddleWare)

	// You can also, create a Stack(), which is a stack
	// of MiddleWare for a specific task
	auth := c.NewStack(CheckUser, CheckToken, ValidSession)

	// Wrap your global middleware with your handler
	http.Handle("/home", c.Use(YourHandler))

	// Add some middleware on a specific handler.
	http.Handle("/", c.Use(YourOtherHandler).Add(OtherMiddle)) 

	// Add a Stack to the route.
	http.Handle("/", c.Use(YourOtherHandler).Stack(auth)) 

	// Start Listening
	http.ListenAndServe(":8080", nil)
}
```

## TODO
- DOC
- Refactoring
- Debugging

## Contributing

1. Fork it
2. Create your feature branch (git checkout -b my-new-feature)
3. Write Tests!
4. Commit your changes (git commit -am 'Add some feature')
5. Push to the branch (git push origin my-new-feature)
6. Create new Pull Request

## License
MIT

## Links

Lightning Fast HTTP Mux : [Bone](https://github.com/go-zoo/bone)
