

## Error Handling in Golang

**What is error handling?**

Error handling is the process of detecting, reporting, and recovering from errors that occur during the execution of a program.

**How to handle errors in Golang?**

There are two ways to handle errors in Golang:

1. **Using the `error` type**

The `error` type is a built-in type in Golang that represents an error. To use the `error` type, you can:

* Define a variable of type `error`.
* Assign an error value to the variable.
* Check the value of the variable to see if an error occurred.
* Use the `fmt.Println()` function to print the error message.

For example:

```go
func divide(a, b int) (int, error) {
  if b == 0 {
    return 0, fmt.Errorf("division by zero: cannot divide %d by %d", a, b)
  }
  return a / b, nil
}

func main() {
  result, err := divide(10, 0)
  if err != nil {
    fmt.Println(err)
  } else {
    fmt.Println(result)
  }
}
```



---

2. **The Blank Identifier (`_`): Ignoring Unwanted Values**

The blank identifier, represented by a single underscore (`_`), is a special construct in Golang used in various scenarios, particularly for discarding unwanted return values from functions.

**Common Uses of the Blank Identifier:**

1. **Ignoring Function Return Values:**

   - When a function returns multiple values, but you only care about a subset, you can use the blank identifier to discard the unused ones. This helps maintain clean and concise code.

   ```go
   func getUserInfo() (string, int, error) {
     name := "Alice"
     age := 30
     err := nil // Assuming no error
     return name, age, err
   }

   func main() {
     username, _, err := getUserInfo()
     if err != nil {
       fmt.Println(err)
       return
     }
     fmt.Println("Username:", username)
   }
   ```

   In this example, `getUserInfo` returns three values: username, age, and error. However, `main` only needs the username. The blank identifier (`_`) discards the age and error values.



**In Summary**

The blank identifier is a versatile tool in Golang for handling unwanted return values, suppressing unused variable errors, and acting as placeholders. Use it effectively to write clean, concise, and well-understood Golang code.
**When to use the `error` type and when to use the `blank identifier`?**

* Use the `error` type when you need to handle the error.
* Use the `blank identifier` when you don't need to handle the error.
