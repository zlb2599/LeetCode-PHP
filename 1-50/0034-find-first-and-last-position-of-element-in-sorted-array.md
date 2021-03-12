# LeetCode 第 34 号问题：在排序数组中查找元素的第一个和最后一个位置

**难度中等**

### 题目描述

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
如果数组中不存在目标值 target，返回 [-1, -1]。
**进阶：**
你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？
**示例 1:**

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

**示例 2:**

```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```

**示例 3:**

```
输入：nums = [], target = 0
输出：[-1,-1]
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
     * @return Integer[]
     */
    function searchRange($nums, $target)
    {
        $n     = count($nums);
        $left  = $this->binarySearch($nums, $n, $target, true);
        $right = $this->binarySearch($nums, $n, $target, false) - 1;
        if ($left <= $right && $right < $n && $nums[$left] == $target && $nums[$right] == $target) {
            $ret[0] = $left;
            $ret[1] = $right;
            return $ret;
        }
        $ret[0] = -1;
        $ret[1] = -1;
        return $ret;
    }

    private function binarySearch(array $nums, $n, $target, $lower)
    {
        $left  = 0;
        $right = $n - 1;
        $ans   = $n;
        while ($left <= $right) {
            $mid = intval(($left + $right) / 2);
            if ($nums[$mid] > $target || ($lower && $nums[$mid] >= $target)) {
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

