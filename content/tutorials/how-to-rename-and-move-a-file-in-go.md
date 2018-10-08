---
title: "How to rename and move a file in go"
date: 2017-09-02T22:43:02+01:00
draft: false
---

To rename a file there is `os.Rename` method, which takes original name and the new name.
```golang
package main

import (
    "fmt"
    "os"
)

func main() {
    oldname := "file1.txt"
    newname := "file2.txt"
    err := os.Rename(oldname, newname)
    if err != nil {
        fmt.Println(err)
    }
}
```

The same method can be used to *move* the file as well.

```golang
package main

import (
    "fmt"
    "os"
)

func main() {
    originalPath := "file1.txt"
    newPath := "/some/other/folder/file2.txt"
    err := os.Rename(originalPath, newPath)
    if err != nil {
        fmt.Println(err)
    }
}
```