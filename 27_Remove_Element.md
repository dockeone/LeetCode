# Question

Given an array and a value, remove all instances of that value in place and return the new length.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

# Thought

***题目的意思：***给定一个数组，以及一个值，把这个数组中的和这个值相等的元素全部移除，然后返回长度。

***思路1：***第一个思路马上就想到了 赛跑的问题，可以让一个 指针先跑，然后把合格的元素给后一个指针，后面的指针就负责重构。

***思路2：***还想到一种思路就是插入排序，把不合格的元素都沉到数组的最后。当然，这种方法的时间复杂度就到了O(n^2)了。

# Solution

```
public class Solution {
    public int removeElement(int[] nums, int val) {
        if((nums == null) || (nums.length == 0)){
            return 0;
        } else {
            int front = 0;
            int back = 0;
            
            for(; front < nums.length; ++front){
                if(nums[front] != val){
                    nums[back++] = nums[front];
                } else {
                    ;
                }
            }
            return back;
        }
    }
}
```




