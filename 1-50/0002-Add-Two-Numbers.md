# LeetCode 第 2 号问题：两数相加

题目来源于 LeetCode 上第 2 号问题：两数相加。题目难度为 Medium。

### 题目描述

给出两个 **非空** 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 **逆序** 的方式存储的，并且它们的每个节点只能存储 **一位** 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例：**

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

### 题目解析

设立一个表示进位的变量`carried`，建立一个新链表，把输入的两个链表从头往后同时处理，每两个相加，将结果加上`carried`后的值作为一个新节点到新链表后面。

### 动画描述

![](/Animation/0002-Add-Two-Numbers.gif)

### 代码实现

```php
/// 时间复杂度: O(n)
/// 空间复杂度: O(n)

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
class Solution
{

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1, $l2)
    {
        $carried   = 0;
        $dummyHead = new ListNode(-1);
        $cur       = &$dummyHead;
        while ($l1 || $l2) {
            $a         = $l1 ? $l1->val : 0;
            $b         = $l2 ? $l2->val : 0;
            $cur->next = new ListNode(($a + $b + $carried) % 10);

            $carried = ($a + $b + $carried) > 9 ? 1 : 0;
            $cur     = &$cur->next;
            $l1      = $l1 ? $l1->next : null;
            $l2      = $l2 ? $l2->next : null;
        }
        $cur->next = $carried ? new ListNode(1) : null;
        return $dummyHead->next;
    }
}

```


