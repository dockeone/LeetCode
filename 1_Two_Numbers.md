# Question


Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

**Example:**

`Given nums = [2, 7, 11, 15], target = 9,`

`Because nums[0] + nums[1] = 2 + 7 = 9,`

`return [0, 1].`

***UPDATE (2016/2/13):***

The return format had been changed to zero-based indices. Please read the above updated description carefully.

Subscribe to see which companies asked this question

# My Thought

***题目的意思是***：给一个数组，有一堆数，然后再给一个数X，问你，在数组中哪个位置和哪个位置相加可以得到 这个数X。

***思路*** 最直接的就是遍历，拿第一个数和以后每个数遍历，然后再拿第二个数字和每个数字遍历，以此类推，总能找出。但是这样子的时间复杂度就变为了 O(n^2). Ps：看 Accepted Solutions Runtime Distribution 的时候，这个算法在 Run Time 中只能打败 19.74 % 的人。
 
怎么才能 ***优化*** 呢，让时间复杂度下降，毕竟这种是最笨的方法。考虑到像Demo 那样，11 和 15 是不可能的，那么就可以首先进行一个排序，排序的话我们可以使用快排，以目标结果X 作为中间点，小于X 的放到前面，这样的时间复杂度是 O(n)。然后我们可以再从小于X的数的前面再用那种最笨的方法进行查找。虽然时间复杂度还是O(n^2)，***但是，这种方式实际上的执行是和 数组内的数字大于目标数X 有很强关联的，也就是说，数组里面有越多大于目标X的数，这个算法效率就越好。 ***

Ps: 这种优化方式有2个缺点：

1. 优化效率依赖于 数组内的数字大于目标数X 的个数。
2. 空间复杂度需要 O(n)，因为题目的意思是找出这个数组中的哪个位置和哪个位置的数，经过排序后，这个位置都乱套了，所以要先 copy 这个数组，空间复杂度就上来了。 但是，如果在业务需求中，只是求哪个数和哪个数，不要求位置，那么这个优化方式还是可以考虑的。


# My Solution


```
package com.test;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int sol[] = new int[2];
        for(int i = 0; i < nums.length - 1; ++i){
            for(int j = i + 1; j < nums.length; ++j){
                int sum = nums[i] + nums[j];
                if(sum == target){
                    sol[0] = i;
                    sol[1] = j;
                    return sol;
                } else {
                    ;
                }
            }
        }
        return null;
    }
}
```

## Discuss Online

在 LeetCode 的 Discuss 中，有人实现了 时间复杂度为 O(n)。
它是怎么做的呢：

```
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < numbers.length; i++) {
        if (map.containsKey(target - numbers[i])) {
            result[1] = i;
            result[0] = map.get(target - numbers[i]);
            return result;
        }
        map.put(numbers[i], i);
    }
    return result;
}
```
这确实用了另外一种思路，就是 通过 哈希表。先把这个数组的数一个个放进 哈希表中，放的同时，判断是不是 a + b = c。这样，后面的数也就不用判断了。这个算法 在 Run Time 为 6ms ，能够打败 58.39% 的人。
但是这种算法 忽略了一点创建 map 是需要空间的。但是整体来说还是要优于傻瓜式的 O(n^2) 的方式。

#Summary

匹配，查找，多考虑下 HashMap 的方式。

