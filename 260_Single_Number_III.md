# Question

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

***Note:***

1. The order of the result is not important. So in the above example, [5, 3] is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

# Thought

***题目意思：*** 给定一个int数组，里面的数大部分都出现了两次，只有2个出现了1次，那么把这两次出现了一次的元素超出来。

***思路：*** 看到两次，重复，下意识的就想到了HashSet，HashMap。

- HashSet: 本来是想 由于HashSet不能放入重复的值，那么假如放入重复的值会抛出异常，但是在实验的过程中没有任何异常，查看内部实现原理也没发现方法上有 throw xxx 。
- HashMap: HashMap可以for循环把数组放入链表中，然后在放的过程中首先判断有没有重复，有的话就不放入，并且把原来的移除出来，最后剩下在HashMap中的就是我们要的值。如下 Solution1 的解法.

***思路2：*** 题目其实建议我们要在 O(n)的时间复杂度，O(1)的空间复杂度来做。时间复杂度上述的思路符合了，但是空间复杂度没有符合，因为知道 HashMap内部会创建 table[]。需要是 O(1)的时间复杂度，那么只能在本身的 int nums[] 中来做。

那么首先它是无顺序的，所以可以先给它排序，***使用快排***，时间复杂度 O(nlogn)，然后nums 数组就会变成 [1,1,2,2,3,5] ，再for循环进行一次挑选，总共时间复杂度为 O(nlogn + n).



# Solution1

```
public class Solution {
    public int[] singleNumber(int[] nums) {

        HashMap<Integer,Integer> hashMap = new HashMap<Integer,Integer>();

        for(int i = 0; i < nums.length; ++i ){
            if(hashMap.get(nums[i]) == null){
                hashMap.put(nums[i],i);
            } else {
                hashMap.remove(nums[i]);
            }
        }

        int retNum[] = new int[2];
        int i = 0;
        for(Map.Entry<Integer,Integer> entry : hashMap.entrySet()){
            retNum[i++] = entry.getKey();
        }
        
        return retNum;
    }
}
```

# Discuss OnLine

```
public class Solution {
    public int[] singleNumber(int[] nums) {
        // Pass 1 : 
        // Get the XOR of the two numbers we need to find
        int diff = 0;
        for (int num : nums) {
            diff ^= num;
        }
        // Get its last set bit
        diff &= -diff;

        // Pass 2 :
        int[] rets = {0, 0}; // this array stores the two numbers we will return
        for (int num : nums)
        {
            if ((num & diff) == 0) // the bit is not set
            {
                rets[0] ^= num;
            }
            else // the bit is set
            {
                rets[1] ^= num;
            }
        }
        return rets;
    }
}
```
表示还没看懂，不过这是 空间复杂度O(1),时间复杂度O(n)。

# Summary

1. HashSet 重复添加不会抛出异常。
