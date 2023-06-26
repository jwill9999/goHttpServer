# Go Http Server

## Default Server Mux 

Here's an example of how to use the `DefaultServeMux` to handle incoming requests:

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "Welcome to the homepage!")
	})

	http.HandleFunc("/about", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "About us")
	})

	http.HandleFunc("/contact", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "Contact us")
	})

	fmt.Println("Starting server on http://localhost:8080")
	http.ListenAndServe(":8080", nil)
}
```

In this example, we register three different handler functions for the routes `/`, `/about`, and `/contact` using the `HandleFunc` method of the `http` package. We then start an HTTP server using the `ListenAndServe` function, passing in `nil` as the second argument to use the `DefaultServeMux`. When a request comes in, the `DefaultServeMux` will match it to the appropriate handler function based on the requested URL path.

## Error handling explained

The first error you’re checking for, http.ErrServerClosed, is returned when the server is told to shut down or close. This is usually an expected error because you’ll be shutting down the server yourself, but it can also be used to show why the server stopped in the output. In the second error check, you check for any other error. If this happens, it will print the error to the screen and then exit the program with an error code of 1 using the os.Exit function.

One error you may see while running your program is the address already in use error. This error can be returned when ListenAndServe is unable to listen on the address or port you’ve provided because another program is already using it. Sometimes this can happen if the port is commonly used and another program on your computer is using it, but it can also happen if you run multiple copies of your own program multiple times. If you see this error as you’re working on this tutorial, make sure you’ve stopped your program from a previous step before running it again.