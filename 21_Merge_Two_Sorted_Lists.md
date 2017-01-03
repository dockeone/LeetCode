# Question

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

# Thought

***题目意思：*** 有两个已经排序好的链表，需要合并成一个链表
***思路：*** 有一个 move 指针，然后可以一直移动。

# Solution

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        } else if(l2 == null){
            return l1;
        } else {
            ListNode head;
            if(l1.val < l2.val){
                head = l1;
            } else {
                head = l2;
            }
            
            while(true){
                ListNode move;
                if(l1.val < l2.val){
                    while(true){
                        if(l1.next == null){
                            break;
                        } else if(l1.next.val <= l2.val){
                            l1 = l1.next;
                        } else {
                            break;
                        }
                    }
                    move = l1.next;
                    l1.next = l2;
                    l1 = move;
                } else {
                    while(true){
                        if(l2.next == null){
                            break;
                        } else if(l2.next.val <= l1.val){
                            l2 = l2.next;
                        } else {
                            break;
                        }
                    }
                    move = l2.next;
                    l2.next = l1;
                    l2 = move;
                }
                
                if(l1 == null || l2 == null){
                    return head;
                } else {
                    ;
                }
            }
        }
    }
}
```

# Discuss 中的递归算法

```
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        }
        if(l2 == null){
            return l1;
        }

        ListNode mergeHead;
        if(l1.val < l2.val){
            mergeHead = l1;
            mergeHead.next = mergeTwoLists(l1.next, l2);
        }
        else{
            mergeHead = l2;
            mergeHead.next = mergeTwoLists(l1, l2.next);
        }
        return mergeHead;
    }
}```

总结：1. 服务器端无论如何都需要做参数验证。2. 尽量看看节省内存



