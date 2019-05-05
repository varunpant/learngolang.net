---
title: "Print Look and Say Sequence in Go"
date: 2019-05-05T23:17:54+01:00
draft: false
---

# Look-and-say sequence

In mathematics, the look-and-say sequence is the sequence of integers beginning as follows:

`1, 11, 21, 1211, 111221, 312211, 13112221, 1113213211, ...` 

To generate a member of the sequence from the previous member, read off the digits of the previous member, counting the number of digits in groups of the same digit. For example:

- **1** is read off as "one 1" or 11.
- **11** is read off as "two 1s" or 21.
- **21** is read off as "one 2, then one 1" or 1211.
- **1211** is read off as "one 1, one 2, then two 1s" or 111221.
- **111221** is read off as "three 1s, two 2s, then one 1" or 312211.

## Here is a code in Golang

```golang
package main

import (
	"fmt"
	"strconv"
)

func main() {

	lookAndSaysequence(10)
}

func lookAndSaysequence(n int) {
	prev := ""
	for i := 0; i < n; i++ {
		if prev == "" {
			prev = "1"
			fmt.Println(prev)
		} else {
			counter := 0
			seen := ""
			tmp := ""
			for _, c := range prev {
				if string(c) == seen {
					counter++
				} else {
					if counter > 0 {
						tmp += strconv.Itoa(counter) + seen
						counter = 0
						seen = ""
					}
					counter = 1
					seen = string(c)
				}

			}

			if counter > 0 {
				tmp += strconv.Itoa(counter) + seen
			}

			prev = tmp
		}
		fmt.Println(prev)
	}
}
```
Execute `go run main.go`

### Result

```
1
1
11
21
1211
111221
312211
13112221
1113213211
31131211131221
13211311123113112211
```