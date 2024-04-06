

**Installing Golang**

1. go to  official Golang website: [https://go.dev/](https://go.dev/) .
2. Download and install Golang based on your operating system.

**Verifying Installation**

1. Open your terminal.
2. Type `go version` and press enter.
3. If Golang is installed correctly, you should see the installed Golang version.

**Golang Workspace and Project Structure**

* Golang uses a specific directory structure for projects called the Go workspace.
* By default, the Go workspace is located in your home directory under a folder named `go`. 
* Inside the `go` folder, there are three subdirectories:
    * `bin`: Stores executable binaries for installed packages.
    * `pkg`: Stores compiled package files.
    * `src`: This is the recommended directory to store your source code (programs).

**Creating a Go Project**

1. Open your terminal and navigate to your desired project directory.
2. Run the command `go mod init <project_name>`, replacing `<project_name>` with your project's name. This initializes a Go module for your project.

**Hello World Program**

1. Create a new file inside the `src` directory of your project and name it `main.go`. This will be your main program file.(optional)
2. Add the following code to `main.go`:

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("Hello, world!")
}
```

* `package main`: Defines the package name for this program.
* `import "fmt"`: Imports the `fmt` package which provides formatting functions like `Println`.
* `func main()`: Defines the main function where the program execution begins.
* `fmt.Println("Hello, world!")`: Prints "Hello, world!" to the console.

**Running the Program**

1. Save the `main.go` file.
2. In your terminal, navigate to the directory containing your `main.go` file.
3. Run the command `go run main.go`.

