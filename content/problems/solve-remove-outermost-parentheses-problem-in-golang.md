---
title: "Remove Outermost Parentheses"
date: 2020-01-10T11:34:26.791419+00:00
draft: false
---

### Remove Outermost Parentheses

#### Problem Statement

A valid parentheses string is either empty **(""), "(" + A + ")"**, or **A + B**, where A and B are valid parentheses strings, and + represents string concatenation.  For example, **"", "()", "(())()", and "(()(()))"** are all valid parentheses strings.

A valid parentheses string S is primitive if it is nonempty, and there does not exist a way to split it into S = A+B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string S, consider its primitive decomposition: **S = P_1 + P_2 + ... + P_k**, where P_i are primitive valid parentheses strings.

Return S after removing the outermost parentheses of every primitive string in the primitive decomposition of S.

**Example 1:**
````bash
Input: "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
````

**Example 2**
````bash
Input: "(()())(())(()(()))"
Output: "()()()()(())"
Explanation: 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
````

**Example 3**
````bash
Input: "()()"
Output: ""
Explanation: 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
````

**Note**

1. **S**.length <= 10000
2. **S**[i] is "(" or ")"
3. **S** is a valid parentheses string




#### Solution

1. We start by ntialising a counter with 0.
2. Next, we scan the string char by char, from left to right.
3. Every time an open parentheses  **(**  is encountered, we increment the counter with 1 and if the count is already greator than 1 indicating (a possible exterior parentheses has already been found), we will add this parentheses to the output string builder.
4. when we encounter a closed parentheses **)**, we decrement the counter and if the counter is greator than 1 (indicating there is more than 1 open parentheses), we can safely add this character to the output string builder.
5. We return the output string after the loop is finished.

```go
package main

import (
	"fmt"
	"strings"
)

func removeOuterParentheses(S string) string {
	var sb strings.Builder
	count := 0
	for _, c := range S {

		if c == '(' {
			if count > 0 {
				sb.WriteString(string(c))
			}
			count++
		}

		if c == ')' {
			if count > 1 {
				sb.WriteString(string(c))
			}
			count--
		}

	}
	return sb.String()
}

func main() {
	fmt.Println(removeOuterParentheses("(()())(())"))
}
```
