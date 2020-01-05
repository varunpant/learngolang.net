---
title: "Reverse Integer"
date: 2020-01-05T07:18:26.791419+00:00
draft: false
---

### Reverse Integer

#### Problem Statement

Given a 32-bit signed integer, reverse digits of an integer.

The general technique here is simple, for a given positive integer:

1. Repeatedly divide by 10 and take the remainder.
2. **x%10** will result in isolating the last number of the digit .
3. **x = x/10** will get rid of the last number for next iteration, *since we use integers and ignore the floating point values*.

##### Example

```bash
123
Reversed = 123%10 = 3 + (0 x 10)  = 3
123/10 = **12**.*3*
```



```bash
12
Reversed = 12%10 = 2 + (3 x 10)  = 32 
12/10 = **1**.*2*
1
```

```
1
Reversed = 1%10 = 1 + (32 x 10)  = 321 
0
```





```go
package main

import "fmt"

func reverse(x int) int {
	res := 0
  //Flag, to remember if the number is negative for later
	isPos := 1
	if x < 0 {
		isPos = -1
    // temporarily convert number to positive
		x = -1 * x
	}
	for {
		if x == 0 {
			break
		}
		res = res*10 + x%10
		if res > 2147483647 {
			return 0
		}
		x /= 10
	}
	return res * isPos

}

func main() {

	fmt.Println(reverse(123))
	fmt.Println(reverse(-123))
	fmt.Println(reverse(120))

}

```

