---
title: "How to write a file in go"
date: 2018-10-05T21:21:19+01:00
draft: false
---

The quickest way to write a file with some bytes is to use `ioutil.WriteFile`

```golang
package main

import (
	"fmt"
	"io/ioutil"
)

func main() {
	err := ioutil.WriteFile("somefile", []byte("foo\n"), 0644)
	if err != nil {
		fmt.Println("error while writing file")
	}
}
```

A more explicit way could be to use `os.Create`

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	f, err := os.Create("foo.dat")
	if err != nil {
		fmt.Println("error while creating file")
	}
	defer f.Close()

	l, err := f.Write([]byte("hello"))
	if err != nil {
		fmt.Println("error while creating file")
	}
	fmt.Printf("wrote %d bytes\n", l)
}
```
If you just want to write some string instead of byte array then just use `WriteString`

```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	f, err := os.Create("foo.dat")
	if err != nil {
		fmt.Println("error while creating file")
	}
	defer f.Close()

	l, err := f.WriteString("foo bar\n")
	if err != nil {
		fmt.Println("error while creating file")
	}
	fmt.Printf("wrote %d bytes\n", l)
}

```
If multiple write operations are performed then make sure to use `f.sync`, to flush writes to stable storage.

Finally its worth mentioning a package `buffio` which helps with [bufferred IO operations](https://www.quora.com/In-C-what-does-buffering-I-O-or-buffered-I-O-mean/answer/Robert-Love-1).

Many small writes can hurt performance, hence a common strategy is to buffer few writes in memory and then write a chunk to the disk as a single block.

```golang
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	f, err := os.Create("foo.dat")
	if err != nil {
		fmt.Println("error while creating file")
	}
	defer f.Close()

	w := bufio.NewWriter(f)
	l, err := w.WriteString("bufferred data\n")
	w.Flush() //write to storge.
	fmt.Printf("wrote %d bytes\n", l)
}
```