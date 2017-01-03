# Question

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

Example:

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

# Thought

***题目的意思：***给定一个 int 型数组，并且有 `1 ≤ a[i] ≤ n`，有些元素出现了两次，其他的都出现了一次。需要找到全部的出现两次的元素，并且不用额外的空间，以及在 O(n) 的时间复杂度。

***思路1：*** 由于是不能创建额外的空间，所以说得在原数组上操作。那么，由于之前接触过位图排序，所以这里可能可以使用到位图排序之类的思路。比如说，`[4,3,2,7,8,2,3,1]` 首先是 4， 表示 4号位，nums[3] = 0（下标从0开始），如果再出现一次，那么就等于 -1，最后统计 -1 的位置即可。

按照这个思路写了1个多小时没写出来，感觉智商还是不够用，伤心ing，但是还是觉得能够实现的。

# Solution

以下为别人的答案，思路是这样子的：利用相反数，如下代码：

```
public class Solution {
    // when find a number i, flip the number at position i-1 to negative. 
    // if the number at position i-1 is already negative, i is the number that occurs twice.
    
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < nums.length; ++i) {
            int index = Math.abs(nums[i])-1;
            if (nums[index] < 0)
                res.add(Math.abs(index+1));
            nums[index] = -nums[index];
        }
        return res;
    }
}
```




