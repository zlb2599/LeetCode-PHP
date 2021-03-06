## LeetCode第12号问题：整数转罗马数字


**级别中等.**

**题目描述：**

```txt
罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。
```
## 题目解析

### 1.贪心

将给定的整数转换为罗马数字需要找到上述 13 个符号的序列，这些符号的对应值加起来就是整数。根据符号值，此序列必须按从大到小的顺序排列。符号值如下。
如概述中所述，表示应该使用尽可能大的符号，从左侧开始工作。因此，使用贪心算法是有意义的。贪心算法是一种在当前时间做出最佳可能决策的算法；在这种情况下，它会取出最大可能的符号。

为了表示一个给定的整数，我们寻找适合它的最大符号。我们减去它，然后寻找适合余数的最大符号，依此类推，直到余数为0。我们取出的每个符号都附加到输出的罗马数字字符串上。

#### 代码实现

```php
//时间复杂度：O(n)
//空间复杂度：O(1)
class Solution
{
  private $digits
        = [
            1000 => "M",
            900  => "CM",
            500  => "D",
            400  => "CD",
            100  => "C",
            90   => "XC",
            50   => "L",
            40   => "XL",
            10   => "X",
            9    => "IX",
            5    => "V",
            4    => "IV",
            1    => "I"
        ];
    /**
     * @param Integer $num
     * @return String
     */
    function intToRoman($num)
    {
        $roman_digits = [];
        # Loop through each symbol.
        foreach ($this->digits as $value => $symbol) {
            if ($num == 0) {
                break;
            }
            $count          = intval($num / $value);
            $num            = $num % $value;
            $roman_digits[] = str_repeat($symbol, $count);
        }
        return join('', $roman_digits);
    }
```
```
