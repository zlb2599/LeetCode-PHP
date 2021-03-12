# LeetCode 第 32 号问题：最长有效括号

**难度中等**

### 题目描述

给你一个只包含 '(' 和 ')' 的字符串，找出最长有效（格式正确且连续）括号子串的长度
**示例 1:**

```
输入：s = "(()"
输出：2
解释：最长有效括号子串是 "()"

```

**示例 2:**

```
输入：s = ")()())"
输出：4
解释：最长有效括号子串是 "()()"
```

**示例 3:**

```
输入：s = ""
输出：0
```


### 题目解析

## 动态规划

### 代码实现

```php
class Solution
{

    /**
     * @param String $s
     * @return Integer
     */
    function longestValidParentheses($s)
    {
        $max = 0;
        $len = strlen($s);
        if ($len == 0) {
            return 0;
        }
        $dp=[];
        for ($i = 1; $i < $len; $i++) {
            if ($s[$i] == ')') {
                if ($s[$i - 1] == '(') {
                    $dp[$i] = ($i >= 2 ? $dp[$i - 2] : 0) + 2;
                } else {
                    if ($i - $dp[$i - 1] > 0 && $s[$i - $dp[$i - 1] - 1] == '(') {
                        $dp[$i] = $dp[$i - 1] +
                                  (($i - $dp[$i - 1]) >= 2 ? $dp[$i - $dp[$i - 1] - 2] : 0) + 2;
                    }
                }
                $max = max($max, $dp[$i]);
            }
        }
        return  $max;
    }
}
```

