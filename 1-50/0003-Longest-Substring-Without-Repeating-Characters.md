# LeetCode 第 3 号问题：无重复字符的最长子串

> 本文首发于公众号「图解面试算法」，是 [图解 LeetCode ](<https://github.com/MisterBooo/LeetCodeAnimation>) 系列文章之一。
>
> 同步博客：https://www.algomooc.com

题目来源于 LeetCode 上第 3 号问题：无重复字符的最长子串。题目难度为 Medium，目前通过率为 29.0% 。

### 题目描述

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```java
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

### 题目解析

建立一个256位大小的整型数组 freg ，用来建立字符和其出现位置之间的映射。

维护一个滑动窗口，窗口内的都是没有重复的字符，去尽可能的扩大窗口的大小，窗口不停的向右滑动。

- （1）如果当前遍历到的字符从未出现过，那么直接扩大右边界；
- （2）如果当前遍历到的字符出现过，则缩小窗口（左边索引向右移动），然后继续观察当前遍历到的字符；
- （3）重复（1）（2），直到左边索引无法再移动；
- （4）维护一个结果res，每次用出现过的窗口大小来更新结果 res，最后返回 res 获取结果。

### 动画描述

![动画描述](/Animation/0003-Longest-Substring-Without-Repeating-Characters)

### 代码实现

```php
// 滑动窗口
// 时间复杂度: O(n)
// 空间复杂度: O(n)
class Solution
{

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLongestSubstring($s)
    {
        $freq = [];
        $l    = 0;
        $r    = -1; //滑动窗口为s[l...r]
        $size = strlen($s);
        $res  = 0;
        while ($l < $size) {
            if ($r + 1 < $size && empty($freq[$s[$r + 1]])) {
                $r++;
                $freq[$s[$r]] = 1;
            } else {   //r已经到头 || freq[s[r+1]] == 1
                $freq[$s[$l]] = 0;
                $l++;
            }
            $res = max($res, $r - $l + 1);
        }
        return $res;
    }
}
```
