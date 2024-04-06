

**Packages**

* Every Golang file belongs to a package.
* The package name is specified in the first line of the file.
* The `main` package is special and contains the `main` function which is the entry point for executable programs.


**Example**

The following code shows how to import the `fmt` package and use it to print "Hello, world!" to the console.

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("Hello, world!")
}
```

**Running the Program**

To run the program, use the `go run` command.

```
go run main.go
```

**Output**

```
Hello, world!
```




**Importing Functions from Subdirectories**

In addition to importing packages from different locations, Golang allows you to import functions from subdirectories within the same folder. This is achieved using relative imports.

**Relative Imports**(go does this automatically)

* Use a single dot (`.`) to refer to the current directory.
* Use double dots (`..`) to refer to the parent directory.

**Example**

Suppose your project directory structure looks like this:

```
project/
  main.go
  utils/
    helper.go
```

The file `main.go` wants to use the `PrintMessage` function defined in `helper.go`. Here's how to import it:

```go
package main

import (
  "./utils" // Import the "utils" package from the current directory's subdirectory
)

func main() {
  utils.PrintMessage("Hello from subdirectory!")
}
```

**Explanation:**

* `./utils`: This imports the `utils` package located in the current directory's subdirectory (`utils`).
* `utils.PrintMessage`: You can then access the `PrintMessage` function from the imported `utils` package.


