# LeetCode 第 29 号问题：串联所有单词的子串

**难度困难**

### 题目描述
给定一个字符串s和一些长度相同的单词words。找出 s 中恰好可以由words 中所有单词串联形成的子串的起始位置。

注意子串要与words 中的单词完全匹配，中间不能有其他字符，但不需要考虑words中单词串联的顺序。


**示例 1:**

```
输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案

```

**示例 2:**

```
输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]

```
### 题目解析

## 滑动窗口

### 代码实现
```php
//时间复杂度：O(n)
class Solution
{

    /**
     * @param String $s
     * @param String[] $words
     * @return Integer[]
     */
    function findSubstring($s, $words)
    {
        if (empty($s) | empty($words)) {
            return [];
        }
        $one_word = strlen($words[0]);
        $word_num = count($words);
        $n        = strlen($s);
        if ($n < $one_word) {
            return [];
        }
        $result = [];
        $m1     = [];
        foreach ($words as $word) {
            $m1[$word]++;
        }
        for ($i = 0; $i < $one_word; $i++) {
            $left  = $i;
            $right = $i;
            $count = 0;
            $m2    = [];
            while ($right + $one_word <= $n) {
                //从s中提取一个单词拷贝到w
                $w     = substr($s, $right, $one_word);
                $right += $one_word;//窗口右边界右移一个单词的长度

                if ($m1[$w] == 0) {//此单词不在words中，表示匹配不成功,然后重置单词个数、窗口边界、以及m2
                    $count = 0;
                    $left  = $right;
                    $m2    = [];
                } else {//该单词匹配成功，添加到m2中
                    $m2[$w]++;
                    $count++;
                    while ($m2[$w] > $m1[$w])//一个单词匹配多次，需要缩小窗口，也就是left右移
                    {
                        $t_w = substr($s, $left, $one_word);
                        $count--;
                        $m2[$t_w]--;
                        $left += $one_word;
                    }
                    if ($count == $word_num) {
                        array_push($result, $left);
                    }
                }
            }
        }
        return $result;
    }
}
```

