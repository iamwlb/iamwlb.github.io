# First_post

## d1

1111

### d111

```go
package main

import (
    "fmt"
    "net/http"
    "time"
)

func greet(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World! %s", time.Now())
}

func main() {
    http.HandleFunc("/", greet)
    http.ListenAndServe(":8080", nil)
}")
```

#### d1111

1111

#### d2222

2222

#### d3333

3333

### d222

222

### d333

333

## d2

22
22
22
22
22
22

## d3

333

## d4

444

