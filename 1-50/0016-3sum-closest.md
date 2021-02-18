# LeetCode 第 16 号问题：最接近的三数之和

**级别中等。**

### 题目描述

给定一个包括n 个整数的数组nums和 一个目标值target。找出nums中的三个整数，使得它们的和与target最接近。返回这三个数的和。假定每组输入只存在唯一答案。


### 题目解析

### 排序 + 双指针

### 代码实现

```php
//时间复杂度：O(N^2)
//空间复杂度：O(logN)。我们忽略存储答案的空间，额外的排序的空间复杂度为 O(logN)。然而我们修改了输入的数组nums，
//在实际情况下不一定允许，因此也可以看成使用了一个额外的数组存储了 nums 的副本并进行排序，空间复杂度为 O(N)。
class Solution
{
    protected $best = PHP_INT_MAX;
    protected $target;

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function threeSumClosest($nums, $target)
    {
        $this->target = $target;
        $n            = count($nums);
        sort($nums);
        for ($first = 0; $first < $n - 2; $first++) {
            $second = $first + 1;
            $third  = $n - 1;
            // 如果当前值和前一个值相同，
            // 则跳过当前循环，防止重复
            if ($first > 0 && $nums[$first] == $nums[$first - 1]) {
                continue;
            }

            while ($second < $third) {
                $sum = $nums[$first] + $nums[$second] + $nums[$third];
                $this->update($sum);
                if ($sum == $target) {
                    return $target;
                } elseif ($sum < $target) {
                    $second++;
                } else {
                    $third--;
                }
            }
        }
        return $this->best;
    }

    private function update($cur)
    {
        if (abs($cur - $this->target) < abs($this->best - $this->target)) {
            $this->best = $cur;
        }
    }
}
```