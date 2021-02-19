# LeetCode 第 29 号问题：两数相除

**难度中等**

### 题目描述
给定两个整数，被除数dividend和除数divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数dividend除以除数divisor得到的商。

整数除法的结果应当截去（truncate）其小数部分，例如：truncate(8.345) = 8 以及 truncate(-2.7335) = -2
**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
解释: 10/3 = truncate(3.33333..) = truncate(3) = 3

```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
解释: 7/-3 = truncate(-2.33333..) = -2
```

### 题目解析

## 二分 + 倍增乘法解法
先实现一个「倍增乘法」，然后利用对于 x 除以 y，结果 x / y 必然落在范围 [0, x] 的规律进行二分：
### 代码实现
```php
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution
{

    /**
     * @param Integer $dividend
     * @param Integer $divisor
     * @return Integer
     */
    function divide($dividend, $divisor)
    {
        if ($dividend == 0) {
            return 0;
        }
        if ($divisor == 1) {
            return $dividend;
        }
        $min = -pow(2, 31);
        $max = pow(2, 31) - 1;
        if ($divisor == -1) {
            if ($dividend > $min) {
                return -$dividend;
            }// 只要不是最小的那个整数，都是直接返回相反数就好啦
            return $max;// 是最小的那个，那就返回最大的整数啦
        }
        $a    = $dividend;
        $b    = $divisor;
        $sign = 1;
        if (($a > 0 && $b < 0) || ($a < 0 && $b > 0)) {
            $sign = -1;
        }
        $a   = $a > 0 ? $a : -$a;
        $b   = $b > 0 ? $b : -$b;
        $res = $this->div($a, $b);
        if ($sign > 0) {
            return $res > $max ? $min : $res;
        }
        return -$res;
    }

    function div($a, $b)
    {  // 似乎精髓和难点就在于下面这几句
        if ($a < $b) {
            return 0;
        }
        $count = 1;
        $tb    = $b; // 在后面的代码中不更新b
        while (($tb + $tb) <= $a) {
            $count = $count + $count; // 最小解翻倍
            $tb    = $tb + $tb; // 当前测试的值也翻倍
        }
        return $count + $this->div($a - $tb, $b);
    }
}
```