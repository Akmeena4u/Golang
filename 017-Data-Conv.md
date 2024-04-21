In Go (Golang), data conversion refers to the process of converting values from one type to another. This can involve converting between basic data types like integers and strings, or converting custom types like structs and slices. Understanding how to perform data conversion is essential for handling data effectively in Go programs. Let's explore data conversion in Go in detail:

### 1. Basic Type Conversions

#### Conversion Syntax:
```go
newType(variable)  // Convert variable to newType
```

#### Example:
```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    // Converting integer to float64
    numInt := 42
    numFloat := float64(numInt)
    fmt.Printf("Integer: %d, Float: %f\n", numInt, numFloat)

    // Converting float64 to int
    pi := 3.14
    approxPi := int(pi)
    fmt.Printf("Float: %f, Integer: %d\n", pi, approxPi)

    // Converting int to string
    age := 30
    ageStr := strconv.Itoa(age)
    fmt.Printf("Age: %d, Age as String: %s\n", age, ageStr)

   // converting string to float
    var str string = "123.45"
    num, err := strconv.ParseFloat(str, 64) // Convert string to float64
   if err == nil {
    fmt.Println(num) // Output: 123.45
   }

}
```

### 2. String Conversions

#### Using `strconv` Package:
The `strconv` package in Go provides functions for converting strings to other types and vice versa.

#### Example:
```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    // Converting string to integer
    ageStr := "25"
    age, err := strconv.Atoi(ageStr)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    fmt.Printf("Age as String: %s, Age as Integer: %d\n", ageStr, age)
}
```

### 3. Custom Type Conversions

#### Conversion between Custom Types:
You can define conversion methods for custom types by implementing methods with receiver types.

#### Example:
```go
package main

import (
    "fmt"
)

type Celsius float64
type Fahrenheit float64

func CToF(c Celsius) Fahrenheit {
    return Fahrenheit(c*9/5 + 32)
}

func FToC(f Fahrenheit) Celsius {
    return Celsius((f - 32) * 5 / 9)
}

func main() {
    boilingC := Celsius(100.0)
    boilingF := CToF(boilingC)
    fmt.Printf("Boiling point in Celsius: %v, Boiling point in Fahrenheit: %v\n", boilingC, boilingF)
}
```

### 4. Type Assertion

#### Checking and Converting Interface Types:
You can use type assertion to check and convert interface types to other specific types.

#### Example:
```go
package main

import (
    "fmt"
)

func printValue(val interface{}) {
    switch v := val.(type) {
    case int:
        fmt.Println("Integer:", v)
    case float64:
        fmt.Println("Float:", v)
    default:
        fmt.Println("Unknown type")
    }
}

func main() {
    printValue(10)            // Integer: 10
    printValue(3.14)          // Float: 3.14
    printValue("hello")       // Unknown type
}
```

### Key Points to Remember:

- Use type conversion syntax (`newType(variable)`) to convert between basic types like int, float, and string.
- Use the `strconv` package for converting strings to other types and handling errors.
- Define custom conversion methods for converting between custom types.
- Use type assertion to check and convert interface types dynamically.

Understanding data conversion in Go is crucial for handling different data types efficiently and effectively within your programs. By mastering data conversion techniques, you'll be able to manipulate and process data seamlessly in your Go applications.
