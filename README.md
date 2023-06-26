# goHttpServer

# Multiplexing Request Handlers

In Go, multiplexing request handlers refer to the ability to handle multiple HTTP requests simultaneously using a single goroutine. This is achieved by using the `ServeMux` type from the `net/http` package to route incoming requests to the appropriate handler function. By using a single goroutine, multiplexing can reduce the overhead of creating and managing multiple goroutines for each incoming request, improving the performance of your web application.

When you started your HTTP server in the last section, you passed the ListenAndServe function a nil value for the http.Handler parameter because you were using the default server multiplexer. Because http.Handler is an interface, it’s possible to create your own struct that implements the interface. But sometimes, you only need a basic http.Handler that calls a single function for a specific request path, like the default server multiplexer. In this section, you will update your program to use http.ServeMux, a server multiplexer and http.Handler implementation provided by the net/http package, which you can use for these cases.

The http.ServeMux struct can be configured the same as the default server multiplexer, so there aren’t many updates you need to make to your program to start using your own instead of a global default. To update your program to use an http.ServeMux, open your main.go file again and update your program to use your own http.ServeMux.

```go

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", getRoot)
	mux.HandleFunc("/hello", getHello)

	err := http.ListenAndServe(":8080", mux)

}

```

In this update, you created a new http.ServeMux using the http.NewServeMux constructor and assigned it to the mux variable. After that, you only needed to update the http.HandleFunc calls to use the mux variable instead of calling the http package. Finally, you updated the call to http.ListenAndServe to provide it the http.Handler you created (mux) instead of a nil value.

```text
go run main.go
```

Your program will continue running as it did last time, so you’ll need to run commands to interact with the server in another terminal. First, use curl to request the / path again:

```
curl http://localhost:8080
```

```
curl http://localhost:8080/hello
```



References: [Multiplexing tutorial](https://www.digitalocean.com/community/tutorials/how-to-make-an-http-server-in-go#multiplexing-request-handlers)