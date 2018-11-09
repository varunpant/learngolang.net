---
title: "How to check file permissions in go"
date: 2018-10-02T22:43:02+01:00
draft: false
---
```golang
package main

import (
	"fmt"
	"os"
)

func main() {
	var perms = []int{os.O_RDONLY, os.O_WRONLY}
	for perm := range perms {
		file, err := os.OpenFile("myFile.txt", perm, 0666)
		if err != nil {
			if os.IsNotExist(err) {
				panic("File not found.")
			}
			if os.IsPermission(err) {
				fmt.Println(fmt.Sprintf("Error: %v permission denied.", perm))
			}
		}
		file.Close()
	}

}

```