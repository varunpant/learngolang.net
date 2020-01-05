---
title: "Two Sum"
date: 2020-01-05T07:17:26.791419+00:00
draft: false
---

### Two Sum

There are obviously many ways to solve this problem, the simplest and least performant a.k.a **brute force** way, is to go from left to right, have two pointers *i* and *i+1* and in a *sliding window* fashion add **arr[i]** with **arr[i+1]**, until we find the match, like shown below

```go
package main

import "fmt"

func twosum(nums []int, target int) []int {
	var a []int

	L := len(nums)
	for i := 0; i < L; i++ {
		for j := i + 1; j < L; j++ {
			if nums[i]+nums[j] == target {
				a = append(a, i, j)
			}
		}

	}
	return a
}

func main() {
	arr := []int{3, 2, 4}
	fmt.Println(twosum(arr, 6))

}

```

There is another approach, which involves putting all values in a ***set*** or a ***dict***  , then iterating the array linearly and checking if **target - current-value** is in the array.

```go
package main

import "fmt"

func twosum(nums []int, target int) []int {
	var a []int
	dict := make(map[int]int)
	L := len(nums)
	for i := 0; i < L; i++ {
		dict[nums[i]] = i
	}
	for i := 0; i < L; i++ {
		lookup := target - nums[i]

		if j, ok := dict[lookup]; ok {
			//Ensure that lookup is not pointing to the current element nums[i]
			if j != i {
				a = append(a, i, j)
				break
			}
		}
	}

	return a
}

func main() {
	arr := []int{3, 2, 4}
	fmt.Println(twosum(arr, 6))

}

```

