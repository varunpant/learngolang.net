---
title: "How to Remove All Files in a Directory in Go"
date: 2018-11-04T12:45:25Z
draft: false
---

### Built in Options

There, always is a need to delete all files in a directory in golang.

`os.RemoveAll` function is used a lot. The documentation says,

>RemoveAll removes path and any children it contains. It removes everything it can but returns the first error it encounters. If the path does not exist, RemoveAll returns nil (no error).

#### Here is a quick example
```golang
func main() {
	err := os.RemoveAll("files")
	fmt.Println(err)
}
```

The issue with `os.RemoveAll('folder')`  is that it also removes the parent `folder` ,(as clearly stated in the doc.)
```golang
os.RemoveAll("/folder/")
```

### Here are few helper methods to create a custom clearDir function.

###  Method 1 (glob)

```golang
package main

import (
	"fmt"
	"os"
	"path/filepath"
)

func main() {

	err := ClearDir("tmp")
	if err != nil {
		fmt.Println(err)
	}
}

func ClearDir(dir string) error {
	files, err := filepath.Glob(filepath.Join(dir, "*"))
	if err != nil {
		return err
	}
	for _, file := range files {
		err = os.RemoveAll(file)
		if err != nil {
			return err
		}
	}
	return nil
}
```

###  Method 2 (ioutil)

Here,we use `ioutil.ReadDir` to get a collection of `os.FileInfo types`, 
next, we iterate through each and remove each child item using `os.RemoveAll.`
 

```golang
package main

import (
	"fmt"
	"io/ioutil"
	"os"
	"path"
)

func main() {
	err := ClearDir("tmp")
	if err != nil {
		fmt.Println(err)
	}

}
func ClearDir(dir string) error {
	names, err := ioutil.ReadDir(dir)
	if err != nil {
		return err
	}
	for _, entery := range names {
		os.RemoveAll(path.Join([]string{dir, entery.Name()}...))
	}
	return nil
}
```

###  Method 3 (os.Open())


```golang
package main

import (
	"fmt"
	"os"
	"path"
)

func main() {
	err := ClearDir("tmp")
	if err!=nil{
		fmt.Println(err)
	}
	
}
func ClearDir(dir string) error {
	dirRead, err := os.Open(dir)
	if err != nil {
		return err
	}
	dirFiles, err := dirRead.Readdir(0)
	if err != nil {
		return err
	}

	// Loop over the  files.
	for index := range dirFiles {
		entery := dirFiles[index]

		// Get name of file and its full path.
		filename := entery.Name()
		fullPath := path.Join(dir, filename)

		// Remove the file.
		os.Remove(fullPath)

		fmt.Println(fullPath)

	}

	return nil
}

```

Hope you find this helpfull.
