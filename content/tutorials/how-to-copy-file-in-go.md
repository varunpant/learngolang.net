---
title: "How to copy a file in go"
date: 2018-01-12T21:21:19+01:00
draft: false
---

Here is a snippet, which copies a file from source to destination.

```golang
package main

import (
	"io"
	"log"
	"os"
)

func main() {

	// Open original file
	source, err := os.Open("foo.txt")
	if err != nil {
		log.Fatal(err)
	}
	defer source.Close()

	// Create new file
	destination, err := os.Create("bar.txt")
	if err != nil {
		log.Fatal(err)
	}
	defer destination.Close()

	// Copy the bytes to destination from source
	bytesWritten, err := io.Copy(destination, source)
	if err != nil {
		log.Fatal(err)
	}
	log.Printf("Copied %d bytes.", bytesWritten)

	// Commit the file contents
	// Flushes memory to disk
	err = destination.Sync()
	if err != nil {
		log.Fatal(err)
	}
}
```