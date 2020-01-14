---

title: "Valid Parentheses"
date: 2020-01-14T07:22:26.791419+00:00
draft: false
---

### Valid Parentheses

#### Problem Statement

Given a string containing just the characters **(** , **)** , **{** , **}**, **[** , **]**

determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```bash
Input: "()"
Output: true
```

**Example 2:**

```bash
Input: "()[]{}"
Output: true
```

**Example 3:**

```bash
Input: "(]"
Output: false
```

**Example 4:**

```bash
Input: "([)]"
Output: false
```

**Example 5:**

```bash
Input: "{[]}"
Output: true
```



#### Solution

Quite simple this one, we need a stack like data structure, then we just need to push if brackets are open and pop if a closed is encountered, then a check if the pope bracket is in order.

```go
func isValid(s string) bool {

	var stack []rune

	for _, brac := range s {
		n := len(stack) - 1

		if brac == '}' {
			if n < 0 {
				return false
			}
			current := stack[n]
			stack = stack[:n]
			if current != '{' {
				return false
			}
		} else if brac == ']' {
			if n < 0 {
				return false
			}
			current := stack[n]
			stack = stack[:n]
			if current != '[' {
				return false
			}
		} else if brac == ')' {
			if n < 0 {
				return false
			}
			current := stack[n]
			stack = stack[:n]
			if current != '(' {
				return false
			}
		} else {
			stack = append(stack, brac)
		}
	}

	if len(stack) == 0 {
		return true
	}
	return false
}
```

