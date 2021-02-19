# LeetCode 第 28 号问题：实现 strStr()

**难度简单**

### 题目描述

实现strStr()函数。

给定一个haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回 -1。
**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```
**说明:**
当needle是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当needle是空字符串时我们应当返回 0 。这与C语言的strstr()以及 Java的indexOf()定义相符。

### 题目解析

## 子串逐一比较 - 线性时间复杂度
最直接的方法 - 沿着字符换逐步移动滑动窗口，将窗口内的子串与 needle 字符串比较。

### 代码实现

```php
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution
{

    /**
     * @param String $haystack
     * @param String $needle
     * @return Integer
     */
    function strStr($haystack, $needle)
    {
        $l = strlen($needle);
        $n = strlen($haystack);

        for ($start = 0; $start < $n - $l + 1; $start++) {
            $str = '';
            $p   = $start;
            while ($p < $start + $l) {
                $str .= $haystack[$p++];
            }
            if ($str == $needle) {
                return $start;
            }
        }
        return -1;
    }
}
```

## 双指针 - 线性时间复杂度

haystack 指针pn，needle 指针pl
首先，只有子串的第一个字符跟 needle 字符串第一个字符相同的时候才需要比较。
其次，可以一个字符一个字符比较，一旦不匹配了就立刻终止。
比较到最后一位时发现不匹配，这时候开始回溯。需要注意的是，pn 指针是移动到 pn = pn - curr_len + 1 的位置，而 不是 pn = pn - curr_len 的位置。


**算法**

- 移动 pn 指针，直到 pn 所指向位置的字符与 needle 字符串第一个字符相等。
- 通过 pn，pL，curr_len 计算匹配长度。
- 如果完全匹配（即 curr_len == L），返回匹配子串的起始坐标（即 pn - L）。
- 如果不完全匹配，回溯。使 pn = pn - curr_len + 1， pL = 0， curr_len = 0。

### 代码实现

```php
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution
{

    /**
     * @param String $haystack
     * @param String $needle
     * @return Integer
     */
    function strStr($haystack, $needle)
    {
        $l = strlen($needle);
        $n = strlen($haystack);

        if ($l == 0) {
            return 0;
        }

        $pn = 0;
        while ($pn < $n - $l + 1) {
            # find the position of the first needle character
            # in the haystack string
            while ($pn < $n - $l + 1 && $haystack[$pn] != $needle[0]) {
                $pn += 1;
            }

            # compute the max match string
            $cur = $pL = 0;
            while ($pL < $l and $pn < $n and $haystack[$pn] == $needle[$pL]) {
                $pn  += 1;
                $pL  += 1;
                $cur += 1;
            }

            # if the whole needle string is found,
            # return its start position
            if ($cur == $l) {
                return $pn - $l;
            }

            # otherwise, backtrack
            $pn = $pn - $cur + 1;
        }
        return -1;
    }
}
```