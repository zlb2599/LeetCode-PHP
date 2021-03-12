# LeetCode 第 31 号问题：下一个排列

**难度中等**

### 题目描述

实现获取 下一个排列 的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。 如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。 必须原地修改，只允许使用额外常数空间。

**示例 1:**

```
输入：nums = [1,2,3]
输出：[1,3,2]

```

**示例 2:**

```
输入：nums = [3,2,1]
输出：[1,2,3]
```

**示例 3:**

```
输入：nums = [1,1,5]
输出：[1,5,1]
```

**示例 4:**

```
输入：nums = [1]
输出：[1]
```

### 题目解析

## 两遍扫描

### 代码实现

```php
class Solution
{

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function nextPermutation(&$nums)
    {
        $len = count($nums);
        $i   = $len - 2;
        while ($i >= 0 && $nums[$i] >= $nums[$i + 1]) {
            $i--;
        }
        if ($i >= 0) {
            $j = $len - 1;
            while ($j >= 0 && $nums[$i] >= $nums[$j]) {
                $j--;
            }
            list($nums[$i], $nums[$j]) = [$nums[$j], $nums[$i]];
        }
        $left  = $i + 1;
        $right = $len - 1;
        while ($left < $right) {
            list($nums[$left], $nums[$right]) = [$nums[$right], $nums[$left]];
            $left++;
            $right--;
        }
    }
}
```

