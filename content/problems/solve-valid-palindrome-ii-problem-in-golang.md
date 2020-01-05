---
title: "Valid Palindrome II"
date: 2020-01-05T09:56:26.791419+00:00
draft: false
---

### Valid Palindrome II

Given a non-empty string *s*, you may delete at most *one* character. Judge whether you can make it a palindrome.

#### Example 1
```
Input: "aba"
Output: True
```

#### Example 2
```
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```


### Solution

This is an easy one, basically compare  *i*th and *length* - *ith* a.k.a *j* chars of the string and move inwards.

If letters do not match , there are two possibilities in this scenario:

1. Deleting/Skipping a leter from L.H.S might result in remaining string to be a valid palendrome.

2. Deleting/Skipping a leter from R.H.S might result in remaining string to be a valid palendrome.

Functioon *isPalindrome* is written to test just that.
 

```go

package main

import "fmt"

func isPalindrome(s string, i int, j int) bool {

	for k := i; k < j; k++ {
		if s[k] != s[j-k+i] {
			return false
		}
	}
	return true
}

func validPalindrome(s string) bool {
	L := len(s)
	for i := 0; i < L/2; i++ {
		if s[i] != s[L-i-1] {
			j := L - i - 1
			if isPalindrome(s, i+1, j) {
				return true
			}
			return isPalindrome(s, i, j-1)

		}
	}
	return true
}

func main() {
	fmt.Println(validPalindrome("abc"))
	fmt.Println(validPalindrome("deeee"))
	fmt.Println(validPalindrome("aba"))
}
```
