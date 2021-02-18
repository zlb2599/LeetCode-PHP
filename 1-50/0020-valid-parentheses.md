# LeetCode 第 20号问题：有效的括号    

**级别简单**

### 题目描述
给定一个只包括 '('，')'，'{'，'}'，'['，']'的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。

**示例 1：**
```
输入：s = "()"
输出：true
```
**示例2：**
```
输入：s = "()[]{}"
输出：true
```
**示例3：**
```
输入：s = "(]"
输出：false
```
**示例4：**
```
输入：s = "([)]"
输出：false
```
**示例5：**
```
输入：s = "{[]}"
输出：true
```

### 题目解析

这道题让我们验证输入的字符串是否为括号字符串，包括大括号，中括号和小括号。

这里我们使用**栈**。

- 遍历输入字符串
- 如果当前字符为左半边括号时，则将其压入栈中
- 如果遇到右半边括号时，**分类讨论：**
- 1）如栈不为空且为对应的左半边括号，则取出栈顶元素，继续循环
- 2）若此时栈为空，则直接返回false
- 3）若不为对应的左半边括号，反之返回false

![](/Animation/0020-valid-parentheses.gif)

### 代码实现

```php
class Solution
{

    private $map
        = [
            ']' => '[',
            '}' => '{',
            ')' => '(',
        ];

    /**
     * @param String $s
     * @return Boolean
     */
    function isValid($s)
    {
        $stack = [];
        $len   = strlen($s);
        for ($i = 0; $i < $len; $i++) {
            if ($s[$i] == '(' || $s[$i] == '{' || $s[$i] == '[') {
                array_push($stack, $s[$i]);
            } else {
                if (empty($stack)) {
                    return false;
                }
                if (array_pop($stack) != $this->map[$s[$i]]) {
                    return false;
                }
            }
        }
        if ($stack) {
            return false;
        }
        return true;
    }
}
```