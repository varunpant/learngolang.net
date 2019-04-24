---
title: "How to solve ransom note problem in go"
date: 2019-04-21T11:21:19+01:00
draft: false
---

Here is a solution using an `array` for solving `ransom note problem` in golang.

```golang
package main

import "fmt"

func main() {
	note := buildCharFrequencyTable("ma said")
	magzine := buildCharFrequencyTable("aaimmds")
	fmt.Println(canBuildNote(note, magzine))
}

func buildCharFrequencyTable(str string) []int {
	counter := []int{
		0, 0, 0, 0,
		0, 0, 0, 0,
		0, 0, 0, 0,
		0, 0, 0, 0,
		0, 0, 0, 0,
		0, 0, 0, 0,
		0, 0,
	}
	for _, char := range str {
		c := int(char - 'a')
		if c > 0 {
			counter[c]++
		}
	}
	return counter
}
func canBuildNote(note []int, magzine []int) bool {
	for i := 0; i < len(magzine); i++ {
		if note[i] > magzine[i] {
			return false
		}
	}
	return true
}

```

Here is another solution to this problem using a hashtable

```golang
package main

import "fmt"

func main() {
	note := buildCharFrequencyTable("ma ssaid")
	magzine := buildCharFrequencyTable("aaimmds")
	fmt.Println(canBuildNote(note, magzine))
}

func buildCharFrequencyTable(str string) map[rune]int {
	dict := map[rune]int{}
	for _, char := range str {
		_, ok := dict[char]
		if ok {
			dict[char]++
		} else {
			dict[char] = 1
		}
	}
	return dict
}
func canBuildNote(note map[rune]int, magzine map[rune]int) bool {
	for k, v := range magzine {
		if note[k] > v {
			return false
		}
	}
	return true
}

```
