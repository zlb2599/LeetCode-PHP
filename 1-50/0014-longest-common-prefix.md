## LeetCode第14号问题：最长公共前缀

**级别简单.**

**题目描述：**

```txt
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。
```

**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

## 题目解析

### 1.分治

#### 代码实现

```php
//时间复杂度：O(mn)
//空间复杂度：O(mlogn)
class Solution
{
    private $strs;

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs)
    {
        if (count($strs) == 0) {
            return "";
        }
        $this->strs = $strs;
        return $this->lcp(0, count($strs) - 1);
    }

    function lcp($start, $end)
    {
        if ($start == $end) {
            return $this->strs[$start];
        }
        $mid       = intval(($start + $end) / 2);
        $left      = $this->lcp($start, $mid);
        $right     = $this->lcp($mid + 1, $end);
        $minLength = min(strlen($left), strlen($right));
        for ($i = 0; $i < $minLength; $i++) {
            if ($left[$i] != $right[$i]) {
                return substr($left, 0, $i);
            }
        }
        return substr($left, 0, $minLength);
    }
}
```

```
