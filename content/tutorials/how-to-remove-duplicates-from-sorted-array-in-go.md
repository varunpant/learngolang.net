---
title: "How to Remove Duplicates From Sorted Array in Go"
date: 2018-11-09T20:02:06Z
draft: false
---

## Problem Statement
Given a sorted array of numbers, remove the duplicates in-place such that each element appear only once and return the new length.

### Example 1
>Given nums = [1,1,2],

>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

>It doesn't matter what you leave beyond the returned length.

### Example 2
>Given nums = [0,0,1,1,1,2,2,3,3,4],

>Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

>It doesn't matter what values are set beyond the returned length.

#### Solution
```golang
import (
	"fmt"
)

func main() {
	fmt.Println(removeDuplicates([]int{1}))
	fmt.Println(removeDuplicates([]int{1, 1, 2}))
	fmt.Println(removeDuplicates([]int{0,0,1,1,1,2,2,3,3,4}))
	fmt.Println(removeDuplicates([]int{1, 1, 2, 3, 4, 5, 5, 6, 7, 8, 8, 8, 9}))
}

func removeDuplicates(nums []int) []int {
	n := len(nums)
	if n <= 1 {
		return nums[0:n]
	}
	j := 1
	for i := 1; i < n; i++ {
		if nums[i] != nums[i-1] {
			nums[j] = nums[i]
			j++
		}
	}

	return nums[0:j]
}
```