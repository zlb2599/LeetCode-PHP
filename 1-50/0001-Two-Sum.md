# LeetCode 第 1 号问题：两数之和


题目来源于 LeetCode 上第 1 号问题：两数之和。题目难度为 Easy。

### 题目描述

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

### 题目解析

使用查找表来解决该问题。

设置一个 map 容器 record 用来记录元素的值与索引，然后遍历数组 nums。

* 每次遍历时使用临时变量 diff 用来保存目标值与当前值的差值
* 在此次遍历中查找 record ，查看是否有与 diff 一致的值，如果查找成功则返回查找值的索引值与当前变量的值 i
* 如果未找到，则在 record 保存该元素与索引值 i

### 动画描述

![](/Animation/0002-Add-Two-Numbers.gif)

### 代码实现

```php
// 1. Two Sum
// https://leetcode.com/problems/two-sum/description/
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution
{

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target)
    {
        $record = [];
        $n      = count($nums);
        for ($i = 0; $i < $n; ++$i) {
            $diff = $target - $nums[$i];
            if (isset($record[$diff])) {
                return [$i, $record[$diff]];
            }
            $record[$nums[$i]] = $i;
        }
        return [];
    }
}

```
