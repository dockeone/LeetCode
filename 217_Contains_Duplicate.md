# Question

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

# Thought

***题目意思：*** 给定一个int型数组，如果有重复的数，那么就 return TRUE，否则就return FALSE；

***思路：*** 直接使用 HashSet，利用Set 不能保存重复的数这一特征，然后判断存入的数的个数和原来的 nums的长度是否相等。

# Solution

```
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet set = new HashSet();
        for(int i = 0; i < nums.length; ++i){
            set.add(nums[i]);
        }
        return set.size() != nums.length;
    }
}
```

# Discuss Online

也是采用 Set 的方法，但是 由于 add 方法如果有重复的话会返回 false。所以上述解决可以稍微改进为：

```
public  boolean containsDuplicate(int[] nums) {
	Set<Integer> set = new HashSet<Integer>();
    for(int i : nums)
             if(!set.add(i))// if there is same
                 return true; 
         return false;
     }
```





