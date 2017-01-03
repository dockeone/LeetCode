# Question

Given two arrays, write a function to compute their intersection.

Example:

Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].

Note:
Each element in the result must be unique.
The result can be in any order.
# Thought

***题目意思：*** 两个数组求交集，不要重复的
***思路：*** 利用 HashMap，第一个数组 put 进去，第二个数组 get 出来 即可。

# Solution

```
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        
        if(nums1 == null || nums2 == null){
            return null;
        } else {
            HashSet<Integer> set = new HashSet<Integer>();
            for (int i = 0; i < nums1.length; i++) {
                set.add(nums1[i]);
            }
    
            Set<Integer> returnSet = new HashSet<Integer>();
    
            for (int i = 0; i < nums2.length; i++) {
                if (set.contains(nums2[i])) {
                    returnSet.add(nums2[i]);
                    set.remove(nums2[i]);
                }
            }
    
            int returnData[] = new int[returnSet.size()];
            Iterator<Integer> iterator = returnSet.iterator();
            int i = 0;
            while(iterator.hasNext()){
                returnData[i++] = iterator.next();
            }
    
            return  returnData;
        }
    }
}```

# Discuss

如果是 内存空间有限，那么先进行二分排序，然后再遍历一个数组，看看是否在另外一个已经排序了的数组中。



