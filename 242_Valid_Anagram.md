# Question

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,

s = "anagram", t = "nagaram", return true.

s = "rat", t = "car", return false.

**Note:**

You may assume the string contains only lowercase alphabets.

**Follow up:**

What if the inputs contain unicode characters? How would you adapt your solution to such case?

# Thought

***题目意思：*** 给予两个字符串 s 和 t，判断 s 和 t 的字符是否相同（包括数量），顺序可以打乱。

***思路：***判断字符是否相同（包括数量），那么就涉及到 double。此时就可以利用 HahsMap， key 是字符， value 是数量。那么先把 s 字符串放入 HashMap，然后 t 再取，进行 remove 操作。最后看这个 hashMap 是否为空。

# Solution

```
public class Solution {
    public boolean isAnagram(String s, String t) {
        if(s == null && t == null) {
            return true;
        } else if(s.length() != t.length()){
            return false;
        } else {
            HashMap<Character,Integer> hashMap = new HashMap<Character, Integer>();

            char schs[] = s.toCharArray();
            char tchs[] = t.toCharArray();

            for(int i = 0; i < s.length(); ++i){
                if(hashMap.get(schs[i]) != null){
                    hashMap.put(schs[i],hashMap.get(schs[i]) + 1);
                } else {
                    hashMap.put(schs[i],1);
                }
            }

            for(int i = 0; i < t.length(); ++i){
                if(hashMap.get(tchs[i]) != null){
                    if(hashMap.get(tchs[i]) != 1){
                        hashMap.put(tchs[i],hashMap.get(tchs[i]) - 1);
                    }else {
                        hashMap.remove(tchs[i]);
                    }
                } else {
                    return false;
                }
            }
            
            if(hashMap.size() != 0) {
                return  false;
            } else {
                return true;
            }
        }
    }
}
```
























