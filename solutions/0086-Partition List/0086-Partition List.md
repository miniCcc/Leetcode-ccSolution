### 题目地址：https://leetcode-cn.com/problems/partition-list/

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例:**

输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5

---

解释：
1. 我们需要找到比x小的所有数，按照相对位置连接在一起
2. 所有大于等于x得数，按照相对位置连接在一起
3. 合并这两个链表，返回结果

### Java
``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode partition(ListNode head, int x) {
        // 加入哑结点，减少了有无头结点的判断
        ListNode maxline = new ListNode(-1);
        ListNode minline = new ListNode(-1);
        ListNode p = head;
        ListNode temp = maxline;
        ListNode temp2 = minline;
        while(p != null){
            ListNode node = new ListNode(p.val);
            if(p.val < x){
                minline.next = node;
                minline = minline.next;
            }else{
                maxline.next = node;
                maxline = maxline.next;
                node.next = null;
            }
            p = p.next;
        }
        minline.next = temp.next;
        return temp2.next;
    }
}
```
