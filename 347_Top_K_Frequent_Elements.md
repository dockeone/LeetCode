# Question


Given a non-empty array of integers, return the k most frequent elements.

For example,
Given [1,1,1,2,2,3] and k = 2, return [1,2].

Note: 
You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

# My Thought

***题目的意思是***：给一个 int 型数组，找出出现最多的 k 个元素，例如 [1,1,1,2,2,3] 以及 k = 2，那么就返回 [1,2]

***思路*** 首先那一个 hashMap记录 key value， 其中 key 就是 元素， value 就是出现的次数，然后进行一个排序即可。

# My Solution


```
public class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; ++i){
            if(map.containsKey(nums[i])){
                map.put(nums[i],map.get(nums[i]) + 1);
            } else {
                map.put(nums[i],1);
            }
        }

        Queue<Map.Entry<Integer,Integer>> queue = new PriorityQueue<>(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {

                Map.Entry<Integer,Integer> _o1 = (Map.Entry<Integer,Integer>) o1;
                Map.Entry<Integer,Integer> _o2 = (Map.Entry<Integer,Integer>) o2;

                if(_o1.getValue() == _o2.getValue()){
                    return 0;
                } else {
                    return _o1.getValue() > _o2.getValue() ? -1 : 1;
                }
            }
        });

        Iterator<Map.Entry<Integer,Integer>> iterator = map.entrySet().iterator();

        while (iterator.hasNext()){
            queue.add(iterator.next());
        }


        List<Integer> list = new LinkedList<>();
        for(int i = 0; i < k; ++i){
            list.add(queue.remove().getKey());
        }

        return list;
    }
}
```