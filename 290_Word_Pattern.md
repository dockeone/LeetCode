# Question

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

**Examples:**

- pattern = "abba", str = "dog cat cat dog" should return true.
- pattern = "abba", str = "dog cat cat fish" should return false.
- pattern = "aaaa", str = "dog cat cat dog" should return false.
- pattern = "abba", str = "dog dog dog dog" should return false.

**Notes:**

You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

**Credits:**

Special thanks to @minglotus6 for adding this problem and creating all test cases.

Subscribe to see which companies asked this question

# My Thought

***题目的意思是：*** 给定一个模式给你，然后给一个字符串给你，分析了这个字符串是不是符合这个模式的，例如：

- pattern = "abba", str = "dog cat cat dog" should return true.
- pattern = "abba", str = "dog cat cat fish" should return false.
- pattern = "aaaa", str = "dog cat cat dog" should return false.
- pattern = "abba", str = "dog dog dog dog" should return false.

***思路：***首先必须要对 字符串转化成一个个单词，放在 数组里面，再判断符不符合模式，当然，也要把模式进行转化成 char[]。然后，其实可以看到，这有点是要用到对应关系的意思，比如 a 对应 dog，b 对应 cat，那么就考虑下 HashMap 的数据结构模式能不能用得上。

那么就有这样一种解法，拿以下举例：
pattern = "abba", str = "dog cat cat dog" should return true.

- 对于pattern第一个a，先用 hashMap.put('a',"dog")
- 对于pattern第二个b：
  - 判断hashMap中有没有b，如果没有，那么判断 b 对应的"dog"和存储在hashMap的 其他key的值是否一样，一样就错了，不一样就对了。如果不一样，那么就 hashMap.put('b',"cat")
  -  如果hashMap中已经有b，那么就判断 hashmap中的b的值和这个 b的值是否一样，不一样就错了，一样就对了。然后，因为hashMap已经有了b，所以就不重复放进去了，继续往下执行。
- 以后依次类推。


# My Solution
```
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        
        //special input control,include "" or null
        //flag = true,it matches; flag = false, it fails.
        boolean flag = isSpecialInputCheck(pattern,str);
        
        if(flag == true){
            if(pattern == null) return true;
            
            String[] chPatts = pattern.split("");
            String[] strs = str.split(" ");
            
            if(chPatts.length != strs.length) return false;
            
            HashMap<String,String> hashMap = new HashMap<String,String>();
            
            for(int i = 0 ; i < chPatts.length; ++i){
                if(hashMap.containsKey(chPatts[i])){
                    if(strs[i].equals(hashMap.get(chPatts[i]))) continue;
                    else flag = false;
                } else {
                    for (Map.Entry<String, String> entry : hashMap.entrySet()) {    
                        if(entry.getValue().equals(strs[i])){
                            flag = false;
                            break;
                        }
                    }  
                    hashMap.put(chPatts[i],strs[i]);
                }
                if(flag == false) break; 
            } 
        }
        return flag;
    }
    
    private boolean isSpecialInputCheck(String pattern, String str){
        if( (pattern == null && str == null) || ("".equals(pattern) && "".equals(str))) {
            return true;
        } else if( (!"".equals(pattern)) && (pattern != null) && (!"".equals(str)) && (str != null) ) {
            return true;
        } else {
            return false;
        }
    }
}
```

# My Solution 2
还有一种方式就是两次 for 循环比较，这种也是感觉比较 恶心的做法，之前这道LeetCode做过一遍，使用的就是这种方式：

```
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        char patterns[] = pattern.toCharArray();
        String strs[] = str.split(" ");
        
        if(patterns.length != strs.length) return false;
        if(patterns.length == 1) return true;
        
        boolean flag = true;
        
        for(int i = 0; i < patterns.length - 1; ++i){
            for(int j = 1; j < patterns.length; ++j){
                flag = patterns[i] == patterns[j] ?
                            strs[i].equals(strs[j]) :
                            !strs[i].equals(strs[j]);
                if( flag == false) return false;
            }
        }
        
        return true;
    }
}
```


# Discuss Online
看了看 Discuss 中别人的解决方案，多数还是和 My Solution 1 一样的解决办法，使用 map。不过他们写的好多都没考虑 null，"" 之类的情况，不知道为什么也能过......





