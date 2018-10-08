---
title: "How to get fileinfo in go"
date: 2017-10-02T22:43:02+01:00
draft: false
---

`os.stat` is used in golang to get all the meta information about a file.

`os.stat` will return a `fileinfo` object or an error if the file is not found.

```golang
package main

import (
	"fmt"
	"log"
	"os"
)

func main() {

	fileInfo, err := os.Stat("myfile.txt")
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("File name:", fileInfo.Name())
	fmt.Println("Size in bytes:", fileInfo.Size())
	fmt.Println("Permissions:", fileInfo.Mode())
	fmt.Println("Last modified:", fileInfo.ModTime())
	fmt.Println("Is Directory: ", fileInfo.IsDir())
	fmt.Printf("System interface type: %T\n", fileInfo.Sys())
	fmt.Printf("System info: %+v\n\n", fileInfo.Sys())

}

```