---
title: "How to create a file in go"
date: 2018-10-05T10:11:33+01:00
draft: false
---

Go lets you easily create and write a new file. 

Here is an example using `create` from `os` package.

```golang
package main

import "os"

func main() {
	//create a file
	f, err := os.Create("foo")
	if err != nil {
		panic(err)
	}
	//make sure it closes.
	defer f.Close()
}
```

`os.Create` creates a file with default mode **0666** , and default file descriptor as **O_RDWR** .

Here is another explicit example

```golang
package main

import "os"

func main() {
	f, err := os.OpenFile("foo", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
	if err != nil {
		panic(err)
	}
	defer f.Close()
}

```