# Question

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

# Thought

***题目的意思：***给定两个非空链表，代表两个非负整数，他们是顺序排列，比如 7243 就是 7->2->4->3 的 list。现在需要把这两个链表加起来，然后返回一个新的结果链表	

***思路：***第一个思路想到的就是由于我们平常做加法的时候都是先做个位，但是这里的链表只能拿到最高位，每次遍历拿到最低位效率太低，所以考虑使用一个后进先出的 queue，这样拿最低位比较好拿。

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

        //转换成链表的数据结构
        LinkedList<ListNode> list_l1 = new LinkedList<>();
        LinkedList<ListNode> list_l2 = new LinkedList<>();

        ListNode flag = l1;
        while(flag != null){
            list_l1.addLast(flag);
            flag = flag.next;
        }
        flag = l2;
        while(flag != null){
            list_l2.addLast(flag);
            flag = flag.next;
        }

        //执行相加
        boolean jinwei = false;
        int a;
        int b;
        int sumAB;
        LinkedList<ListNode> returnNodeHead = new LinkedList<>();
        while(true){

            if(list_l1.isEmpty()){
                addInEmpty(returnNodeHead,list_l2,jinwei);
                break;
            }
            if(list_l2.isEmpty()){
                addInEmpty(returnNodeHead,list_l1,jinwei);
                break;
            }

            a = list_l1.removeLast().val;
            b = list_l2.removeLast().val;
            sumAB = jinwei ? a + b + 1 : a + b;
            jinwei = sumAB >= 10 ? true : false;
            returnNodeHead.addFirst(new ListNode(sumAB >= 10 ? sumAB - 10 : sumAB));
        }

        //把 returnNodeHead 转换成 ListNode 的数据结构
        ListNode returnNode = new ListNode(0);
        flag = returnNode;
        Iterator<ListNode> listNodeIterator = returnNodeHead.iterator();
        while (listNodeIterator.hasNext()){
            flag.next = listNodeIterator.next();
            flag = flag.next;
        }

        return returnNode.next;
    }
    
    private static void addInEmpty(LinkedList<ListNode> returnNodeHead, LinkedList<ListNode> list, boolean jinwei) {
         int a;
        int sum;

        //如果需要进位,那么则需要考虑是否会循环进位
        if(jinwei == true){
            while(true){
                if(list.isEmpty()){
                    returnNodeHead.addFirst(new ListNode(1));
                    break;
                }
                a = list.removeLast().val;
                sum = jinwei ? a + 1 : a;
                jinwei = sum >= 10 ? true : false;
                returnNodeHead.addFirst(new ListNode(sum >= 10 ? sum - 10 : sum));

                if(jinwei == false){
                    break;
                }
            }
        }

        //如果不需要进位,那么就直接把 queue 中的元素 copy
        for(int i = list.size() - 1 ; i >= 0; --i){
            returnNodeHead.addFirst(list.get(i));
        }
    }
}```




