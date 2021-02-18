## LeetCode第11号问题：盛水最多的容器


**级别中等**

**题目描述：**

```txt
给你n个非负整数a1，a2，...，an，每个数代表坐标中的一个点(i,ai)。在坐标内画n条垂直线，
垂直线i的两个端点分别为(i,ai)和(i,0)。找出其中的两条线，使得它们与x轴共同构成的容器可以容纳最多的水。
说明：你不能倾斜容器，且n的值至少为2。
示例：
输入：[1,8,6,2,5,4,8,3,7]
输出：49
```
## 题目解析

我们都应该听说过**木桶原理**，一个木桶可以装入多少水取决于最短的那块板；而这道题也可以与木桶装水的问题对应上。
 很容易的可以得到---->**容器可以容纳水的容量=两条垂直线中最短的那条*两条线之间的距离**
 现在的情况是，有很多条线，让你计算两两之间能装的最多的水，其实暴力法之间就能解决这个问题，但是它的时间复杂度也达到了**O(n^2)**

ok


### 1.双指针

思路：使用两个指针（**resource**和**last**）分别指向数组的第一个元素和最后一个元素，然后我们计算这两条“线”之间能容纳的水的容量，
并更新最大容量（初始值为0）；接着我们需要将指向元素值小的那个指针前移一步，然后重复上面的步骤，直到**resource = last**循环截止。

**GIF动画演示：**

![](/Animation/0011-maxArea.gif)

#### 代码实现

```php
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution
{
    public function maxArea($height)
    {
        $resource = 0;
        $last     = count($height) - 1;
        $res      = 0;
        while ($resource < $last) {
            if ($height[$resource] >= $height[$last]) {
                $res = max($res, ($last - $resource) * $height[$last]);
                $last--;
            } else {
                $res = max($res, ($last - $resource) * $height[$resource]);
                $resource++;
            }
        }
        return $res;
    }
}
```
