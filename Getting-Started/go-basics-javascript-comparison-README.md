# Why Go Is Useful — Beginner Notes

These notes explain the main ideas from the lesson in simple language, with comparisons to JavaScript.

---

## 1. Go Is Simple and Clear

Go is designed to be easy to read and understand.

### JavaScript

```javascript
let name = "Sam";
console.log(name);
```

### Go

```go
package main

import "fmt"

func main() {
    name := "Sam"
    fmt.Println(name)
}
```

Go may look slightly more strict, but that makes large programs easier to understand and maintain.

**Main idea:** Go prefers simple and predictable code.

---

## 2. JavaScript Runs Through Node.js

A JavaScript file normally needs Node.js to run.

```bash
node main.js
```

Flow:

```text
main.js
   ↓
Node.js loads the file
   ↓
The JavaScript engine processes it
   ↓
The program runs
```

Your computer does not normally run `main.js` directly. It uses Node.js.

A deployed JavaScript backend usually needs:

- JavaScript files
- Node.js
- Installed npm packages

---

## 3. Go Is Compiled

Go source code is compiled before it runs.

```bash
go build
```

Flow:

```text
main.go
   ↓
Go compiler reads and checks the code
   ↓
Machine code is generated
   ↓
main.exe is created
```

You can then run the executable:

```bash
main.exe
```

The computer does not need Go installed just to run the already compiled executable.

> A Windows `.exe` normally cannot run directly on Linux. Programs are compiled for a particular operating system and processor.

**Main difference:**

- JavaScript normally runs through Node.js.
- Go can be compiled into a native executable.

---

## 4. How Go Catches Errors Before Creating the Executable

Before generating `main.exe`, the Go compiler checks your source code.

```text
Read code
   ↓
Check syntax
   ↓
Check variable types
   ↓
Check function arguments and returns
   ↓
Check names and imports
   ↓
Create executable
```

If a check fails, compilation stops.

### Wrong type example

```go
package main

func main() {
    age := 23
    age = "twenty-three"
}
```

The compiler remembers that `age` is an integer.

Then it sees that you are trying to put a string into it.

It reports an error similar to:

```text
cannot use "twenty-three" as int value in assignment
```

No executable is created until you fix the error.

### JavaScript comparison

```javascript
let age = 23;
age = "twenty-three";
```

JavaScript allows the variable to change from a number to text.

This flexibility is useful, but some mistakes may only appear while the program is running.

---

## 5. Types of Errors

### Compile-time error

The compiler finds the problem before the program runs.

Example:

```go
age := 23
age = "hello"
```

### Runtime error

The program starts, but a problem happens while it is running.

### Logic error

The program runs, but the result is wrong.

```go
price := 100
quantity := 2

total := price - quantity
```

This code is valid, but perhaps you intended:

```go
total := price * quantity
```

The compiler cannot always know your intention.

**Important:** Go catches many errors early, but it cannot catch every mistake.

---

## 6. Static Typing

Go is statically typed.

That means a variable has a specific type, and Go checks that type before the program runs.

```go
age := 23
```

Here, Go understands that `age` is an integer.

You cannot later put text into it:

```go
age = "twenty-three"
```

### JavaScript

JavaScript is dynamically typed:

```javascript
let age = 23;
age = "twenty-three";
```

### Simple comparison

| JavaScript | Go |
|---|---|
| Dynamically typed | Statically typed |
| A variable can change type | A variable keeps its type |
| Some type errors appear at runtime | Many type errors are caught before running |

---

## 7. “Batteries Included”

“Batteries included” means Go already provides many useful tools in its standard library.

Go includes packages for:

- Creating HTTP servers
- Reading and writing files
- Working with JSON
- Testing
- Dates and time
- Cryptography
- Database connections

### JavaScript example

In Node.js, developers often install external packages:

```bash
npm install express
```

Then Express is used to create a server.

### Go example

Go can create a basic server using its built-in `net/http` package:

```go
package main

import (
    "fmt"
    "net/http"
)

func home(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello")
}

func main() {
    http.HandleFunc("/", home)
    http.ListenAndServe(":8080", nil)
}
```

No separate web-server package is required for this basic example.

**Main idea:** Go already gives you many backend tools.

---

## 8. High Performance

Go programs are compiled into machine code before running.

This helps Go perform well for:

- Backend servers
- APIs
- Networking tools
- Cloud software
- Programs that process a lot of work

JavaScript can also be fast, especially because Node.js uses the V8 engine, but Go is commonly chosen when predictable performance and efficient server-side work are important.

---

## 9. Concurrency

Concurrency means:

> A program can manage multiple tasks during the same period.

Example:

```text
User 1 → waiting for the database
User 2 → logging in
User 3 → requesting products
```

The server does not need to remain idle while User 1 is waiting. It can work on another request.

### JavaScript

JavaScript commonly uses:

- The event loop
- Promises
- `async`
- `await`

### Go

Go commonly uses:

- Goroutines
- Channels

A goroutine is a lightweight task managed by the Go runtime.

```go
go doSomething()
```

The `go` keyword starts the function as a goroutine.

You will study goroutines later. For now, remember:

```text
JavaScript → async/await and event loop
Go         → goroutines and channels
```

Concurrency is useful for:

- Handling multiple web requests
- Calling several APIs
- Reading multiple files
- Running background jobs
- Downloading or processing data

**Main idea:** Concurrency helps a program manage multiple tasks efficiently.

---

## 10. Overall Comparison

| Topic | JavaScript | Go |
|---|---|---|
| How it runs | Normally through Node.js | Compiles into an executable |
| Typing | Dynamic | Static |
| Error checking | Some errors appear at runtime | Many errors are caught during compilation |
| Concurrency | Event loop, promises, async/await | Goroutines and channels |
| Packages | Often uses npm packages | Strong standard library |
| Common use | Frontend and backend | Backend, APIs, cloud, networking |

---

## Final Summary

Go is useful because it is:

- Simple and readable
- Statically typed
- Compiled
- Fast
- Good at handling many tasks
- Equipped with a strong standard library
- Able to catch many mistakes before the executable is created

The most important ideas from this lesson are:

1. JavaScript normally needs Node.js to run.
2. Go can compile source code into an executable.
3. The Go compiler checks the code before creating the executable.
4. Static typing catches many type mistakes early.
5. “Batteries included” means Go already has many useful built-in packages.
6. Concurrency helps Go manage multiple requests or tasks efficiently.

---

## Self-Check Questions

Try to answer these without looking above:

1. Why does JavaScript normally need Node.js?
2. What does `go build` do?
3. Why might Go refuse to create an executable?
4. What is static typing?
5. What does “batteries included” mean?
6. What does concurrency mean?
7. What is one difference between JavaScript concurrency and Go concurrency?
8. Can the compiler catch every logic error?

If you can explain these in your own words, you understand this topic well.
