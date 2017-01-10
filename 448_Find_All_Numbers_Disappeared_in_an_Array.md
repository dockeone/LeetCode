# Question

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

# Thought

***题目的意思：***给定一个 int 型数组，其中 `1 ≤ a[i] ≤ n` ，n是数组的长度，有些元素出现了两次，有些出现一次。需要找出所有的在 `[1, n]` 中没有出现过的元素。

***思路：***第一个思路马上就想到了利用相反数，因为以前好像有一道题就是这样做的。

# Solution

```
public class Solution {
    public char findTheDifference(String s, String t) {
        Map<Character,Integer> map = new HashMap<>();

        for(int i = 0; i < t.length(); ++i){
            if(map.containsKey(t.charAt(i))){
                map.put(t.charAt(i),map.get(t.charAt(i)) + 1);
            } else {
                map.put(t.charAt(i),1);
            }
        }

        for(int i = 0; i < s.length(); ++i){
            if(map.get(s.charAt(i)) == 1){
                map.remove(s.charAt(i));
            } else {
                map.put(s.charAt(i),map.get(s.charAt(i)) - 1);
            }
        }
       
        Iterator<Map.Entry<Character, Integer>> iterator = map.entrySet().iterator();
        return iterator.next().getKey();
    }
}
```




