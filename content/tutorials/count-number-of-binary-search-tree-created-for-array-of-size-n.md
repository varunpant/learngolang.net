---
title: "Count number of binary search tree created for array of size n"
date: 2018-11-09T21:47:32Z
draft: false
---

This problem is an example of ["catalan Numbers problem"](https://learngolang.net/tutorials/find-nth-catalan-number-in-golang/)

The Question is as follows *Count number of binary search tree created for array of size n*

### Solution in golang

```golang
package main

import (
	"fmt"
)

func main() {

	for i := 0; i < 20; i++ {
		fmt.Println(i, countTreesRec(i))
	}

}

func countTreesRec(numKeys int) int {
	if numKeys <= 1 {
		return 1
	} else {
		sum := 0

		for root := 1; root <= numKeys; root++ {
			left := countTreesRec(root - 1)
			right := countTreesRec(numKeys - root)
			sum += left * right
		}
		return sum
	}
}

```