# 题目

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

# 思路

***题目的意思是：*** 给定一个链表，并且给出一个链表中的某一个节点，要求你删除该节点。

***思路：*** 感觉这题难度不是特别大。删除这个点，平常如果能拿到整个链表的话，直接拿该节点的前一个节点连接到该节点的后一个节点。但是现在只能拿到该节点，所以说不能用这种方式。但是我们可以把后面的值赋值到该节点中来，for循环遍历一遍即可。

# 解决方法

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
    public void deleteNode(ListNode node) {
        
        if(node == null || node.next == null) return ;
        
        while(node.next.next != null) {
            node.val = node.next.val;
            node = node.next;
        }
        node.val = node.next.val;
        node.next = null;
    }
}
```

# 重新思考

后来再回过头来看，上术的思路是对的，但是实现有很严重的问题，为什么要 while 循环呢，其实

```
node.val=node.next.val;
node.next=node.next.next;
```

这样就 ok 了。












