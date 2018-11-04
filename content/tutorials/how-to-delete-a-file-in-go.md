---
title: "How to delete a file in go"
date: 2018-10-02T22:43:02+01:00
draft: false
---

The os package has `os.Remove` function, which is used to delete a file as shown below.

```golang
package main

import (
    "fmt"
    "os"
)

func main() {
    err := os.Remove("test.txt")
    if err != nil {
        fmt.Println(err)
    }
}
```