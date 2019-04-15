---
title: "How to convert number to roman numerals"
date: 2019-04-15T11:21:19+01:00
draft: false
---

### Summary

Converting integers to markdown is fairly simple.

Here are **13** roman numerals and their decimal equivalent.

| Decimal       | Roman         |
| ------------- |:-------------:|
| 1             | I            |
| 4             | IV           |
| 5             | V            |
| 9             | IX           |
| 10            | X            |
| 40            | XL           |
| 50            | L            |
| 90            | XC           |
| 100           | C            |
| 400           | CD           |
| 500           | D            |
| 900           | CM           |
| 1000          | M            |

The process is as follows, for any given decimal number **X**:

1. *From the table shown above*, find the **highest** decimal value, **V**, that is less than or equal to decimal number **X** i.e. **V<=X**.
2.  Write the roman numeral **N** that was found and subtract its value **V** from **X**:


### Integer to Roman in golang.

```golang
package main

import (
	"fmt"
)

func main() {

	for i := 0; i < 100; i++ {
		fmt.Println(i, intToRoman(i))
	}

}

func intToRoman(num int) string {
	values := []int{
		1000, 900, 500, 400,
		100, 90, 50, 40,
		10, 9, 5, 4, 1,
	}

	symbols := []string{
		"M", "CM", "D", "CD",
		"C", "XC", "L", "XL",
		"X", "IX", "V", "IV",
		"I"}
	roman := ""
	i := 0
	for num > 0 {
		k := num / values[i]
		for j := 0; j < k; j++ {
			roman += symbols[i]
			num -= values[i]
		}
		i++
	}
	return roman
}
```

Lets annotate this code, to make things a bit more clear.

```golang

func intToRoman(num int) string {
	values := []int{
		1000, 900, 500, 400,
		100, 90, 50, 40,
		10, 9, 5, 4, 1,
	}

	symbols := []string{
		"M", "CM", "D", "CD",
		"C", "XC", "L", "XL",
		"X", "IX", "V", "IV",
		"I"}
	roman := ""
	i := 0
	
	for num > 0 {
		// calculate the number of times this num is completly divisible by values[i]
		// times will only be > 0, when num >= values[i]
		k := num / values[i]
		for j := 0; j < k; j++ {
			//buildup roman numeral
			roman += symbols[i]
			
			//reduce the value of num.
			num -= values[i]
		}
		i++
	}
	return roman
}
```
