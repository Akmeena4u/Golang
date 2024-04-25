Handling web requests in Go (Golang) involves using the `net/http` package, which provides robust functionality for building HTTP servers and making HTTP client requests. Let's break down the key concepts with simplified explanations and examples.

### Creating an HTTP Server

To create an HTTP server, use `http.ListenAndServe` to specify the address and handler for incoming requests.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!") // Send response to client
}

func main() {
    http.HandleFunc("/", handler) // Register handler for the root route
    fmt.Println("Server listening on port 8080...")
    http.ListenAndServe(":8080", nil) // Start the HTTP server
}
```

- **Explanation**: 
  - We define a handler function (`handler`) that writes "Hello, World!" back to the client's response writer (`w`).
  - We register this handler with `http.HandleFunc` to handle requests coming to the root URL (`"/"`).
  - The `http.ListenAndServe` function starts the server on port `8080`.

### Making HTTP Client Requests

To make HTTP requests as a client, use `http.Get` to fetch data from a URL.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    url := "https://jsonplaceholder.typicode.com/posts/1"
    response, err := http.Get(url)
    if err != nil {
        fmt.Printf("HTTP request failed: %v\n", err)
        return
    }
    defer response.Body.Close()

    body, err := ioutil.ReadAll(response.Body)
    if err != nil {
        fmt.Printf("Failed to read response body: %v\n", err)
        return
    }

    fmt.Println("Response Body:", string(body))
}
```

- **Explanation**: 
  - We use `http.Get` to fetch data from a URL (`url`).
  - We handle any errors that occur during the request.
  - We read the response body using `ioutil.ReadAll` and print it out.

### Handling Different HTTP Request Methods

In an HTTP server, you can handle different request methods (`GET`, `POST`, etc.) using `http.HandleFunc` and a switch statement.

```go
func handler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
    case "GET":
        fmt.Fprintf(w, "Received GET request")
    case "POST":
        fmt.Fprintf(w, "Received POST request")
    default:
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
    }
}
```

- **Explanation**: 
  - We check the HTTP request method (`r.Method`) using a switch statement inside the handler function.
  - Depending on the method (`GET`, `POST`, etc.), we perform different actions or return an error response.

### Using a Router for Advanced Routing

For more complex routing and request handling, use `github.com/gorilla/mux` package.

```go
package main

import (
    "fmt"
    "net/http"

    "github.com/gorilla/mux"
)

func main() {
    r := mux.NewRouter()
    r.HandleFunc("/", homeHandler).Methods("GET")
    r.HandleFunc("/users/{id}", getUserHandler).Methods("GET")

    fmt.Println("Server listening on port 8080...")
    http.ListenAndServe(":8080", r)
}

func homeHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Welcome to the home page!")
}

func getUserHandler(w http.ResponseWriter, r *http.Request) {
    vars := mux.Vars(r)
    userID := vars["id"]
    fmt.Fprintf(w, "User ID: %s", userID)
}
```

- **Explanation**: 
  - We use `github.com/gorilla/mux` for advanced routing capabilities.
  - We define specific routes (`"/"` and `"/users/{id}"`) and corresponding handler functions (`homeHandler` and `getUserHandler`).

### Sending JSON Responses

To send JSON responses from an HTTP server, use `encoding/json` package.

```go
package main

import (
    "encoding/json"
    "net/http"
)

type User struct {
    ID   int    `json:"id"`
    Name string `json:"name"`
}

func main() {
    http.HandleFunc("/user", getUser)
    http.ListenAndServe(":8080", nil)
}

func getUser(w http.ResponseWriter, r *http.Request) {
    user := User{ID: 1, Name: "John Doe"}
    jsonResponse, err := json.Marshal(user)
    if err != nil {
        http.Error(w, "Failed to marshal JSON", http.StatusInternalServerError)
        return
    }
    w.Header().Set("Content-Type", "application/json")
    w.Write(jsonResponse)
}
```

- **Explanation**: 
  - We define a `User` struct with JSON tags.
  - In the `getUser` handler, we marshal a `User` instance into JSON and set appropriate headers.

### Error Handling

Always handle errors properly when making HTTP requests or building HTTP servers in Go.

```go
response, err := http.Get("https://example.com")
if err != nil {
    http.Error(w, "Internal Server Error", http.StatusInternalServerError)
    return
}
defer response.Body.Close()
```

- **Explanation**: 
  - We check for errors after making an HTTP request (`http.Get`).
  - If an error occurs, we return an appropriate HTTP error response.

### Summary

- Building HTTP servers and making client requests in Go involves using the `net/http` package.
- For more complex routing and request handling, consider using third-party packages like `github.com/gorilla/mux`.
- Always handle errors properly and use appropriate response formats (e.g., JSON) for web applications.
