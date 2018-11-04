---
title: "Linking and symlink a file in go"
date: 2018-10-02T21:21:19+01:00
draft: false
---

A **Link** in **Linux** is just a pointer to a file or a directory.

A **hardlink** is a **new pointer** to the same file,
 **hard links** actually have file contents.

A **softlink** does not point directly to the file, and is only a reference. **softlinks** are also called **symlink**


### Hard Linking in golang

```golang
package main

import (
	"fmt"
	"os"
)

func main() {

	err := os.Link("original.txt", "hardlink.txt")
	if err != nil {
		fmt.Println(err)
	}
}
```
### Soft Linking in golang.

```golang
package main

import (
	"fmt"
	"os"
)

func main() {

	err := os.Symlink("original.txt", "softlink.txt")
	if err != nil {
		fmt.Println(err)
	}
}
```
>Symlinks are not supported in Windows