---
title: "Remove Element"
date: 2020-01-16T07:25:26.791419+00:00
draft: false
---

### Remove Element

#### Problem Statement

Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

#### Solution

To solve this, 

1. We will take a pointer **p**, which will point to the first element of the array.
2. We will scan the array from left to right, and every time the target value **val** is encountered, we will continue (indicting no action required.)
3. Otherwise keep on copying the values at **nums[i]** to **nums[pos]**.

When there is no matching value in the array, **pos** will shadow **i**, if there is a match, then **i** will skip a count for matching indices, in next iteration, the non matching adjacent values will simply "shift left" onto it.

````go
package main

import "fmt"

func removeElement(nums []int, val int) int {
	pos := 0
	for i := 0; i < len(nums); i++ {
		if nums[i] == val {
		} else {
			nums[pos] = nums[i]
			pos++
		}

	}
	nums = nums[0:pos]

	return len(nums)
}
func main() {
	arr := []int{3, 2, 2, 3}
	p := removeElement(arr, 3)
	fmt.Println(p)

}
````



