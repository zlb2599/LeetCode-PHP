# LeetCode 第 7 号问题：整数反转

题目来源于 LeetCode 上第 7 号问题：整数反转。题目难度为 Easy。


## 题目描述

给你一个 32 位的有符号整数 x ，返回 x 中每位上的数字反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。

## 示例

```
Example 1:
输入：x = 123
输出：321
Example 2:
输入：x = -123
输出：-321
Example 3:
输入：x = 120
输出：21
Example 4:
输入：x = 0
输出：0

```

## 题目解析

我们可以一次构建反转整数的一位数字。在这样做的时候，我们可以预先检查向原整数附加另一位数字是否会导致溢出。

反转整数的方法可以与反转字符串进行类比。

我们想重复“弹出” xx 的最后一位数字，并将它“推入”到 \text{rev}rev 的后面。最后，\text{rev}rev 将与 xx 相反。

要在没有辅助堆栈 / 数组的帮助下 “弹出” 和 “推入” 数字，我们可以使用数学方法。

//pop operation:
pop = x % 10;
x /= 10;

//push operation:
temp = rev * 10 + pop;
rev = temp;

#### 代码实现

```php
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function reverse($x)   {
        $rev = 0;
        $max = pow(2, 31) - 1;
        $mix = -pow(2, 31);
        while ($x != 0) {
            $pop = $x % 10;
            $x   = intval($x / 10);
            if ($rev > $max / 10 || ($rev == $max / 10 && $pop > 7)) {
                return 0;
            }
            if ($rev < $mix / 10 || ($rev == $mix / 10 && $pop < -8)) {
                return 0;
            }
            $rev = $rev * 10 + $pop;
        }
        return $rev;
    }
}
```