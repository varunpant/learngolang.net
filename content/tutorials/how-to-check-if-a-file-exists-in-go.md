---
title: "How to check if a file exists in go"
date: 2018-10-01T18:02:05+01:00
draft: false
---

Here is a quick snippet to check if a file exists in go

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	if _, err := os.Stat("somefile"); os.IsNotExist(err) {
		fmt.Println("path to \"somefile\" does not exist")
	}
}
```
In an edge case a file might disappear between an **exist** check and **open**

So, it might be a good idea to always open a file and check for returned `err`.

If the file does not exist, it can be detected by `os.IsNotExist(err)` and  non-existence can be handled there.

A better approach could be use `os.OpenFile` and try to **open** or **create** a file. This would only throw an error if a file already exists.

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	f, err := os.OpenFile("ff", os.O_RDWR|os.O_CREATE|os.O_EXCL, 0666)
	if err != nil {
		if os.IsExist(err) {
			fmt.Println("file already exists.")
		}

	}
	defer f.Close()
}

```