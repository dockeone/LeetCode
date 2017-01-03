# Question

Given an array of size n, find the majority element. The majority element is the element that appears more than  n/2  times.

You may assume that the array is non-empty and the majority element always exist in the array.

# Thought

***题目意思：*** 给定一个 数组，找出元素，该元素需要出现至少 n/2 次。

***思路：*** 直接使用 HashMap即可。key 为该元素， value 为出现的次数。最后再遍历一遍找出出现超过 n/2 的即可。

# Solution

```
public class Solution {
    public int majorityElement(int[] nums) {
        HashMap<Integer,Integer> hashMap = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length ;++i){
            if(hashMap.get(nums[i]) == null){
                hashMap.put(nums[i],1);
            } else {
                hashMap.put(nums[i],hashMap.get(nums[i]) + 1);
            }
        }

        return majorityElement0(hashMap);
    }
    
    private static int majorityElement0(HashMap<Integer, Integer> nums) {

        int nowKey = 0;
        int nowValue = 0;

        for(Map.Entry entry : nums.entrySet()){
            if((int)entry.getValue() > nowValue){
                nowKey = (int)entry.getKey();
                nowValue = (int)entry.getValue();
            } else {
                ;
            }
        }
        return  nowKey;
    }
}
```





