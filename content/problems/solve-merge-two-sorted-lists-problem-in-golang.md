---
title: "Merge Two Sorted Lists"
date: 2020-01-15T07:23:26.791419+00:00
draft: false
---

### Merge Two Sorted Lists

#### Problem

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```bash
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```



#### Solution

````go
package main

import "fmt"

type ListNode struct {
	Val  int
	Next *ListNode
}

func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
	var a *ListNode
	pos := &ListNode{Val: -1, Next: nil}
	a = pos
	for {
		if l1 != nil && l2 != nil {

			if l1.Val <= l2.Val {
				pos.Next = l1
				l1 = l1.Next
			} else {
				pos.Next = l2
				l2 = l2.Next
			}
			pos = pos.Next
		} else {
			break
		}

	}
	if l1 != nil {
		pos.Next = l1
	}
	if l2 != nil {
		pos.Next = l2
	}

	return a.Next

}

func main() {

	l1 := &ListNode{
		Val: 1, Next: &ListNode{
			Val: 2,
			Next: &ListNode{
				Val:  4,
				Next: nil,
			},
		},
	}

	l2 := &ListNode{
		Val: 1, Next: &ListNode{
			Val: 3,
			Next: &ListNode{
				Val:  4,
				Next: nil,
			},
		},
	}

	mergeTwoLists(l1, l2)

}

````

