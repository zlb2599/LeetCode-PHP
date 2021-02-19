# LeetCode 第 24 号问题：两两交换链表中的节点

**难度困难**

### 题目描述

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

**示例:**

```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

### 题目解析

## 1迭代
- 设置一个虚拟头结点`dummyHead `
- 设置需要交换的两个节点分别为`node1 `、`node2`，同时设置`node2`的下一个节点`next`

##### 在这一轮操作中

- 将`node2`节点的next设置为`node1`节点
- 将`node1`节点的next设置为`next `节点
- 将`dummyHead `节点的next设置为`node2 `
- 结束本轮操作

接下来的每轮操作都按照上述进行。

### 动画描述

![动画演示](/Animation/0024-Swap-Nodes-in-Pairs.gif)

### 代码实现

```php
// 时间复杂度: O(n)
// 空间复杂度: O(1)
class Solution
{
    /**
     * @param ListNode $head
     * @return ListNode
     */
    function swapPairs($head)
    {
        $dummyHead       = new ListNode(0);
        $dummyHead->next = $head;

        $p = $dummyHead;
        while ($p->next && $p->next->next) {
            $node1       = $p->next;
            $node2       = $node1->next;
            $next        = $node2->next;
            $node2->next = $node1;
            $node1->next = $next;
            $p->next     = $node2;
            $p           = $node1;
        }

        return $dummyHead->next;
    }
}

```


