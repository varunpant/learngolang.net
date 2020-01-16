---
title: "Roman to Integer"
date: 2020-01-16T07:20:26.791419+00:00
draft: false
---

### Roman to Integer

#### Problem Statement

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

**Example 1:**

```
Input: "III"
Output: 3
```

**Example 2:**

```
Input: "IV"
Output: 4
```

**Example 3:**

```
Input: "IX"
Output: 9
```

**Example 4:**

```
Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 5:**

```
Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

#### Solution

Iterate the string from left to right, while maintaining three variables, current, preventive and total. According to roman number rules, if the current variable is gator then previously encountered then **total = total - 2* prev** , otherwise just keep on suing them as they are encountered. Note a map of individual numerals to numbers is maintained.



````go
package main

import "fmt"

func romanToInt(s string) int {
	roman := map[string]int{
		"I": 1,
		"V": 5,
		"X": 10,
		"L": 50,

		"C": 100,
		"D": 500,
		"M": 1000,
	}
	prev, total := 0, 0
	for _, c := range s {
		curr := roman[string(c)]
		total += curr
		
      if curr > prev {
        total -= 2 * prev
      }
      prev = curr

	}
	return total
}
func main() {

	fmt.Println(romanToInt("LVIII"))
	fmt.Println(romanToInt("IX"))

}

````

