---
title: "Find Nth Catalan Number in Golang"
date: 2018-11-09T20:52:48Z
draft: false
---

# Compute n'th Catalan number

In combinatorial mathematics, the Catalan numbers form a sequence of natural numbers that occur in various counting problems, often involving recursively-defined objects. They are named after the Belgian mathematician Eugène Charles Catalan.

They can be computed using this formula:

`C(2n, n)/(n + 1)`

Read more about them [here](http://mathforum.org/advanced/robertd/catalan.html)


### Recursive code in go

```golang
func main() {

	for i := 0; i < 20; i++ {
		fmt.Println(i, catalan(i))
	}
	//0 1
	//1 1
	//2 2
	//3 5
	//4 14
	//5 42
	//6 132
	//7 429
	//8 1430
	//9 4862
	//10 16796
	//11 58786
	//12 208012
	//13 742900
	//14 2674440
	//15 9694845
	//16 35357670
	//17 129644790
	//18 477638700
	//19 1767263190

}

// catalan(n) is sum of catalan(i)*catalan(n-i-1)
func catalan(n int) int {
	// Base case
	if n <= 1 {
		return 1
	}

	res := 0
	for i := 0; i < n; i++ {
		res += catalan(i) * catalan(n-i-1)
	}

	return res
}
```

### Using Binomial Coefficient

We can also use the below formula to find nth catalan number in O(n) time.


```golang
package main

import (
	"fmt"
)

func main() {

	for i := 0; i < 20; i++ {
		fmt.Println(i, catalan(i))
	}

}

// BinomialCoefficient calculates the value of [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
func binomialCoefficient(n int, k int) int {
	res := 1

	// Since C(n, k) = C(n, n-k)
	if k > n-k {
		k = n - k
	}

	for i := 0; i < k; i++ {
		res *= (n - i)
		res /= (i + 1)
	}

	return res
}

// A Binomial coefficient based function to find nth catalan
// number in O(n) time
func catalan(n int) int {
	// Calculate value of 2nCn
	c := binomialCoefficient(2*n, n)

	// return 2nCn/(n+1)
	return c / (n + 1)
}
```
