# LeetCode 第 19号问题：删除链表的倒数第 N 个结点

**级别中等。**

### 题目描述

给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

进阶：你能尝试使用一趟扫描实现吗？

**示例1：**
```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```
**示例2：**
```
输入：head = [1], n = 1
输出：[]
```
**示例1：**
```
输入：head = [1,2], n = 1
输出：[1]
```

### 题目解析

我们可以设想假设设定了双指针`p`和`q`的话，当`q`指向末尾的`NULL`，`p`与`q`之间相隔的元素个数为`n`时，那么删除掉`p`的下一个指针就完成了要求。

- 设置虚拟节点`dummyHead`指向`head`
- 设定双指针`p`和`q`，初始都指向虚拟节点`dummyHead`
- 移动`q`，直到`p`与`q`之间相隔的元素个数为`n`
- 同时移动`p`与`q`，直到`q`指向的为`NULL`
- 将`p`的下一个节点指向下下个节点

![](/Animation/0019-remove-nth-node-from-end-of-list.gif)

### 题目解析

### 双指针

### 代码实现

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $n
     * @return ListNode
     */
    function removeNthFromEnd($head, $n)
    {
        $dummyHead = new ListNode(-1, $head);
        $p         =& $dummyHead;
        $q         =& $dummyHead;
        for ($i = 0; $i < $n; $i++) {
            $p =& $p->next;
        }
        while ($p->next) {
            $p = &$p->next;
            $q = &$q->next;
        }
        $del_node = $q->next;
        $q->next  = $del_node->next;

        return $dummyHead->next;
    }
}
```

