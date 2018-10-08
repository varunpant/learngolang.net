---
title: "How to truncate a file in go"
date: 2018-10-05T22:33:21+01:00
draft: false
---

Truncating a file is very rare but incase yer wondering how to do it in go, here is a snippet.

This code will truncate a file to 50 bytes. 
If the file is less than 50 bytes the original contents will remain
at the beginning, and the rest of the space is filled will null bytes. 

If it is over 50 bytes, then everything after 50 bytes will be lost.  
  
`Truncate` ensures that the file size is exactly as specified. 

*Pass in 0 to truncate to a completely empty file*

```golang
package main

import (
    "log"
    "os"
)

func main() {
    
    err := os.Truncate("foo.text", 50)
    if err != nil {
        log.Fatal(err)
    }
}
```