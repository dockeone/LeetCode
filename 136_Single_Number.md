# Question
---

Given an array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

# Thought
---

题目意思： 给定一个 int 数组，全部的数都出现了两次，只有一个数只出现一次，找到这个数。

思路： 由于最好不要创建额外的空间，那么只能在原数组中做。而且需要接近线性的时间，所以个人感觉首先是要先排序，比如说快排的时间复杂度为 O(nlogn)，再遍历查找即可 O(n)。

# Solution
---

```
public class Solution {
    public int singleNumber(int[] nums) {
        
        if(nums.length == 1) return nums[0];
        
        sort(nums,0,nums.length - 1);
        
        return doFindSingleNumber(nums);
    }
    
    public int doFindSingleNumber(final int nums[]){
        for(int i = 0; i < nums.length - 1; i = i + 2){
            if(nums[i] != nums[i + 1]){
                return nums[i];
            }
        }
        return nums[nums.length - 1];
    }
    
    public void sort(int nums[],
                     final int START,
                     final int END){
        int i = START;
        int j = END;
        int flag = nums[START];
        
        while(i < j){
            while( (i < j) && (nums[j] >= flag) ){
                j--;
            };
            nums[i] = nums[j];
            while( (i < j) && (nums[i] <= flag) ){
                i++;
            };
            nums[j] = nums[i];
        }
        nums[i] = flag;
        
        if( (i - START) > 1 ) sort(nums,START,i - 1);
        if( (END - i) > 1 ) sort(nums, i + 1,END);
    }
}
```

# 重新解决

---

像这类问题，可以使用异或来解决。主要是利用了 

`x ^ x = 0` 

以及 

`x ^ 0 = x` 

那么就会有 

`x ^ y ^ y ^ z ^ z .... = x`

这样就可以求出这个单一的 x。代码如下：

```
public static char findTheDifference(String s, String t) {
    int result = 0;
    for(int i = 0 ; i < s.length(); ++i){
        result ^= s.charAt(i);
    }

    for(int i = 0; i < t.length(); ++i){
        result ^= t.charAt(i);
    }

    return (char) result;
}
```