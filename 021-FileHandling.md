File handling in Go (Golang) involves working with files on the filesystem, including tasks like reading from files, writing to files, creating files, deleting files, and more. Go provides a rich set of functions and types in the `os` and `io/ioutil` packages for efficient file handling.

### 1. Opening and Closing Files

To work with files, you typically start by opening them. The `os.Open` function is commonly used to open a file for reading:

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("example.txt")
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    defer file.Close() // Ensure the file is closed when function returns

    // File operations go here (reading, writing, etc.)
}
```

Similarly, to create or open a file for writing, use `os.Create`:

```go
file, err := os.Create("output.txt")
if err != nil {
    fmt.Println("Error creating file:", err)
    return
}
defer file.Close()
```

### 2. Reading from Files

You can read from a file using `os.Open` or `ioutil.ReadFile`:

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    data, err := ioutil.ReadFile("example.txt")
    if err != nil {
        fmt.Println("Error reading file:", err)
        return
    }
    fmt.Println("File contents:")
    fmt.Println(string(data))
}
```

### 3. Writing to Files

To write data to a file, use `os.OpenFile` with appropriate permissions or `ioutil.WriteFile`:

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    content := []byte("Hello, Golang!")
    err := ioutil.WriteFile("output.txt", content, 0644)
    if err != nil {
        fmt.Println("Error writing to file:", err)
        return
    }
    fmt.Println("Data written to file successfully.")
}
```

### 4. Reading and Writing Line by Line

To read or write line by line, you can use a `Scanner` for reading or a `Writer` for writing:

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    // Reading from a file line by line
    file, err := os.Open("example.txt")
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    defer file.Close()

    scanner := bufio.NewScanner(file)
    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }

    // Writing to a file line by line
    outputFile, err := os.Create("output.txt")
    if err != nil {
        fmt.Println("Error creating file:", err)
        return
    }
    defer outputFile.Close()

    writer := bufio.NewWriter(outputFile)
    _, err = writer.WriteString("Line 1\n")
    if err != nil {
        fmt.Println("Error writing to file:", err)
        return
    }
    _, err = writer.WriteString("Line 2\n")
    if err != nil {
        fmt.Println("Error writing to file:", err)
        return
    }

    // Flush to ensure all buffered operations are applied
    writer.Flush()
}
```

### 5. Checking File Existence and File Information

You can check if a file exists and get its information using `os.Stat`:

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    fileInfo, err := os.Stat("example.txt")
    if err != nil {
        if os.IsNotExist(err) {
            fmt.Println("File does not exist.")
        } else {
            fmt.Println("Error:", err)
        }
        return
    }

    fmt.Println("File Name:", fileInfo.Name())
    fmt.Println("File Size (bytes):", fileInfo.Size())
    fmt.Println("Permissions:", fileInfo.Mode())
    fmt.Println("Is Directory?", fileInfo.IsDir())
    fmt.Println("Modification Time:", fileInfo.ModTime())
}
```

### 6. Deleting Files

To delete a file, use `os.Remove`:

```go
err := os.Remove("example.txt")
if err != nil {
    fmt.Println("Error deleting file:", err)
    return
}
fmt.Println("File deleted successfully.")
```

### 7. Working with Directories

For working with directories (creating, reading, deleting), use functions from the `os` package (`Mkdir`, `MkdirAll`, `ReadDir`, `Remove`, etc.).

### Summary

File handling in Go is straightforward due to the well-designed standard library. Always handle errors properly when dealing with file operations, and make sure to close files using `defer` or `file.Close()` to avoid resource leaks. The examples above cover common file handling tasks in Go, but the standard library provides more functionality for advanced file operations.
