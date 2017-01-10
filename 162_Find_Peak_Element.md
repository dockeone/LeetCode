# Question

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.


# Thought

***题目的意思：***一个 peak element 就是指这个元素比它相邻的元素都要大。给定一个数组，其中 `num[i] ≠ num[i+1]`，需要找到这个 peak element，并且返回它的坐标。一个数组可能会有很多个，那么就返回其中一个都 ok。另外，假定 ` num[-1] = num[n] = -∞`。

例如：`[1, 2, 3, 1]` 的 peak element 就是 3，那么就应该返回索引 2。

***思路：***第一个思路马上就想到那就分 左，中，右三个数，那么需要注意这次的中和右的比较，其实就是下一次的左和中的比较，需要复用这个。

# Solution

```
public class Solution {
    public int findPeakElement(int[] nums) {
        if((nums.length == 1) || (nums[1] < nums[0])){
            return 0;
        }

        boolean nextLeftGreaterThanMiddle = nums[1] > nums[0];
        for(int i = 1; i < nums.length - 1; ++i){
            if(nums[i] > nums[i + 1]){
                if(nextLeftGreaterThanMiddle == true){
                    return  i;
                }
                nextLeftGreaterThanMiddle = false;
            } else if(nums[i] == nums[i + 1]){
                nextLeftGreaterThanMiddle = false;
            } else {
                nextLeftGreaterThanMiddle = true;
            }
        }

        return nums.length - 1;
    }
}
```

# Top Solution

看了一下 top solution，发现我这种实现需要 O(n)的时间复杂度，但是其实可以使用二分法找到最大值，那么最大值其实肯定就是 peak element了。这样时间复杂度还是 O(lgn)，效率会高一些。



