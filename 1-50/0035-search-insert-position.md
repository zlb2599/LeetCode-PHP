# LeetCode 第 35 号问题：在排序数组中查找元素的第一个和最后一个位置

**难度简单**

### 题目描述

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
你可以假设数组中无重复元素。

**示例 1:**

```
输入: [1,3,5,6], 5
输出: 2
```

**示例 2:**

```
输入: [1,3,5,6], 2
输出: 1
```

**示例 3:**

```
输入: [1,3,5,6], 7
输出: 4
```

### 题目解析

## 二分查找

### 代码实现

```php
//时间复杂度： O(logn)
//空间复杂度： O(1)
class Solution
{

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function searchInsert($nums, $target)
    {
        $n     = count($nums);
        $left  = 0;
        $right = $n - 1;
        $ans   = $n;
        while ($left <= $right) {
            $mid = (($right - $left) >> 1) + $left;
            if ($nums[$mid] >= $target) {
                $right = $mid - 1;
                $ans   = $mid;
            } else {
                $left = $mid + 1;
            }
        }
        return $ans;
    }
}
```

