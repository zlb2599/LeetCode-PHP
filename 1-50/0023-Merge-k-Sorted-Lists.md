# LeetCode 第 23 号问题：合并 K 个排序链表

**难度困难**

### 题目描述

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

**示例:**

```
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6

```

### 题目解析

### 题目分析一

这里需要将这 *k* 个排序链表整合成一个排序链表，也就是说有多个输入，一个输出，类似于漏斗一样的概念。

因此，可以利用最小堆的概念。

取每个 Linked List 的最小节点放入一个 heap 中，排序成最小堆。然后取出堆顶最小的元素，放入输出的合并 List 中，然后将该节点在其对应的 List 中的下一个节点插入到 heap
中，循环上面步骤，以此类推直到全部节点都经过 heap。

由于 heap 的大小为始终为 k ，而每次插入的复杂度是 logk ，一共插入了 nk 个节点。时间复杂度为 O(nklogk)，空间复杂度为O(k)。

### 动画演示

![动画演示](/Animation/0023-Merge-k-Sorted-Lists.gif)

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
     * @param ListNode[] $lists
     * @return ListNode
     */
       function mergeKLists($lists)
    {
        if (empty($lists)) {
            return [];
        }
        $dummyHead = new ListNode(null);//虚拟头结点
        $p         = $dummyHead;
        $heap      = new SplMinHeap();//最小堆
        foreach ($lists as $key => $item) {
            while ($item) {
                $heap->insert($item->val);//加入堆中
                $item = $item->next;
            }
        }
        while (!$heap->isEmpty()) {     //依次拿出所有数据
            $p->next = new ListNode($heap->extract());
            $p       = $p->next;
        }

        return $dummyHead->next;  //返回结果

    }
}
```

### 题目分析二

这道题需要合并 k 个有序链表，并且最终合并出来的结果也必须是有序的。如果一开始没有头绪的话，可以先从简单的开始：**合并 两 个有序链表**。

合并两个有序链表：将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

这道题目按照题目描述做下去就行：新建一个链表，比较原始两个链表中的元素值，把较小的那个链到新链表中即可。需要注意的一点时由于两个输入链表的长度可能不同，所以最终会有一个链表先完成插入所有元素，则直接另一个未完成的链表直接链入新链表的末尾。

现在回到一开始的题目：合并 K 个排序链表。

**合并 K 个排序链表** 与 **合并两个有序链表** 的区别点在于操作有序链表的数量上，因此完全可以按照上面的代码思路来实现合并 K 个排序链表。

这里可以参考 **归并排序 **的分治思想，将这 K 个链表先划分为两个 K/2 个链表，处理它们的合并，然后不停的往下划分，直到划分成只有一个或两个链表的任务，开始合并。

### 代码实现

根据上面的动画，实现代码非常简单也容易理解，先划分，直到不能划分下去，然后开始合并。

```php
class Solution {
    function mergeKLists($lists){
    $len=count($lists);
        if($len == 0)
            {return null;}
        if($len == 1)
            {return $lists[0];}
        if($len == 2){
           return $this->mergeTwoLists($lists[0],$lists[1]);
        }

        $mid =intval( $len/2);
        $l1 = new ListNode[$mid];
        for($i = 0; $i < $mid; $i++){
            $l1[$i] = $lists[$i];
        }

        $l2 = new ListNode[$len-$mid];
        for($i = $mid,$j=0; $i < $len; $i++,$j++){
            $l2[$j] = $lists[$i];
        }

        return $this->mergeTwoLists($this->mergeKLists($l1),$this->mergeKLists($l2));

    }
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
