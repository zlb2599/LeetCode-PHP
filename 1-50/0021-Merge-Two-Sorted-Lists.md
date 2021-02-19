# LeetCode 第 21 号问题：合并两个有序链表

**难度简单**

### 题目描述

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

### 题目解析

####  一般方案

##### 1.1 解题思想

> （1）对空链表存在的情况进行处理，假如 pHead1 为空则返回 pHead2 ，pHead2 为空则返回 pHead1。（两个都为空此情况在pHead1为空已经被拦截）
> （2）在两个链表无空链表的情况下确定第一个结点，比较链表1和链表2的第一个结点的值，将值小的结点保存下来为合并后的第一个结点。并且把第一个结点为最小的链表向后移动一个元素。
> （3）继续在剩下的元素中选择小的值，连接到第一个结点后面，并不断next将值小的结点连接到第一个结点后面，直到某一个链表为空。
> （4）当两个链表长度不一致时，也就是比较完成后其中一个链表为空，此时需要把另外一个链表剩下的元素都连接到第一个结点的后面。

##### 1.2 代码实现

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
class Solution
{

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2)
    {
        if (is_null($l1)) {
            return $l2;
        } elseif (is_null($l2)) {
            return $l1;
        }
        if ($l1->val < $l2->val) {
            $new_head = $l1;
            $l1       = $l1->next;
        } else {
            $new_head = $l2;
            $l2       = $l2->next;
        }

        $tail =& $new_head;
        while ($l1 && $l2) {
            if ($l1->val < $l2->val) {
                $tail->next = $l1;
                $l1         = $l1->next;
            } else {
                $tail->next = $l2;
                $l2         = $l2->next;
            }
            $tail =& $tail->next;
        }
        if (is_null($l1)) {
            $tail->next = $l2;
        } elseif (is_null($l2)) {
            $tail->next = $l1;
        }
        return $new_head;
    }
}
```

#### 2 递归方案

##### 2.1 解题思想

> （1）对空链表存在的情况进行处理，假如 pHead1 为空则返回 pHead2 ，pHead2 为空则返回 pHead1。
> （2）比较两个链表第一个结点的大小，确定头结点的位置
> （3）头结点确定后，继续在剩下的结点中选出下一个结点去链接到第二步选出的结点后面，然后在继续重复（2 ）（3） 步，直到有链表为空。

##### 2.2 代码实现

```php
class Solution
{

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2)
    {
        $new_head=null;
        if (is_null($l1)) {
            return $l2;
        } elseif (is_null($l2)) {
            return $l1;
        }
        if ($l1->val < $l2->val) {
            $new_head = $l1;
            $new_head->next      = $this->mergeTwoLists($l1->next,$l2);
        } else {
            $new_head = $l2;
            $new_head->next      = $this->mergeTwoLists($l1,$l2->next);
        }
        return  $new_head;

    }
}
```

