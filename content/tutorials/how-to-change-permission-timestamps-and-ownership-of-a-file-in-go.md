---
title: "How to change permission, timestamps and ownership of a file in go"
date: 2018-10-05T21:21:19+01:00
draft: false
---

### Change Permission

Package `os`, has a handy `Chmod` method, just like the command line interface in **Linux** .

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	err := os.Chmod("myfile.txt", 0777)
	if err != nil {
		fmt.Println(err)
	}
}
```

### Change Ownership

There is also a `Chown`

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	err := os.Chown("myFile.txt", os.Getuid(), os.Getgid())
	if err != nil {
		fmt.Println(err)
	}
}
```

### Change timestamps

As well as a `Chtimes`

```golang
package main

import (
	"fmt"
	"os"
	"time"
)

func main() {

	later := time.Now().Add(24 * time.Hour)
	lastAccessTime := later
	lastModifyTime := later
	err := os.Chtimes("myFile.txt", lastAccessTime, lastModifyTime)
	if err != nil {
		fmt.Println(err)
	}
}
```