# Question

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example:**

Given 1->2->3->4->5->NULL,

return 1->3->5->2->4->NULL.

**Note:**

The relative order inside both the even and odd groups should remain as it was in the input. 
The first node is considered odd, the second node even and so on ...

**Credits:**

Special thanks to @DjangoUnchained for adding this problem and creating all test cases.

Subscribe to see which companies asked this question

# My Thought

***题目的意思是：*** 有一个链表，我们要对它进行重新排序，单数位置的放前面，双数的放后面，空间复杂度要是O(1)，时间复杂度要是O(n).

***思路：***比较容易想到，单数的作为一个链表，双数的作为一个链表，然后再把双数的链表拼接在单数的链表的后面。

- 对于空间复杂度是O(1)，所以说肯定是在原链表的基础上操作，最多就定义多几个Node来记录下位置。
- 对于时间复杂度是O(n)，其实只要是for循环一遍下来，单数的归类到单数链表，双数的归类到双数链表，for循环结束后，再把双数的链表拼接在单数的链表的后面。就能保证是 O(n) 的了。


# My Solution

```
package com.test;

public class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null || head.next == null || head.next.next == null){
            return head;
        } else {
            ListNode odd = head;
            ListNode evenHead = head.next;
            ListNode even = evenHead;
            
            ListNode flag = evenHead;
            int i = 0;
            while(flag.next != null){
                flag = flag.next;
                
                if(i == 0){
                    odd.next = flag;
                    odd = odd.next;
                    i = 1;
                } else if(i == 1){
                    even.next = flag;
                    even = even.next;
                    i = 0;
                }
            }
            odd.next = evenHead;
            even.next = null;
            return head;
        }
    }

    class ListNode {
    	int val;
   	 	ListNode next;
   	 	ListNode(int x) { val = x; }
    }
}	
```

## Discuss Online
和 Discuss 中的答案相比，上述的这个算法 思路是正确的，但是就是显得太啰嗦了，如下比较简介的代码：

```
public class Solution {
public ListNode oddEvenList(ListNode head) {
    if (head != null) {

        ListNode odd = head, even = head.next, evenHead = even; 

        while (even != null && even.next != null) {
            odd.next = odd.next.next; 
            even.next = even.next.next; 
            odd = odd.next;
            even = even.next;
        }
        odd.next = evenHead; 
    }
    return head;
}}
```







