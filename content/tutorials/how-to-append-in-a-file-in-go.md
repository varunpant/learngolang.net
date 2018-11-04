---
title: "How to append in a file in go"
date: 2018-10-05T22:20:24+01:00
draft: false
---

Here is a snippet which shows how to append data in a file in golang. 

We will use `os.OpenFile` with `os._APPEND` flag.

```golang
package main

import (
	"fmt"
	"os"
)

func main() {

	for i := 0; i < 10; i++ {
		append(fmt.Sprintf("line %d \n", i))
	}
}

func append(text string) {
	f, err := os.OpenFile("myfile.txt", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
	if err != nil {
		panic(err)
	}
	defer f.Close()
	f.WriteString(text)
}
```

Here is a handly list of other flags which can be combined togther and used

| Flag        | Description                |
|-------------|----------------------------|
| os.O_RDONLY | Read only                  |
| os.O_WRONLY | Write only                 |
| os.O_RDWR   | Read and write             |
| os.O_APPEND | Append to end of file      |
| os.O_CREATE | Create is none exist       |
| os.O_TRUNC  | Truncate file when opening |