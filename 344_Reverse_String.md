# Question

Write a function that takes a string as input and returns the string reversed.

Example:
Given s = "hello", return "olleh".

# Thought

***题目意思：*** 对一个字符串进行翻转
***思路：*** 拆分，然后 StringBuilder 从后往前再 append。

# Solution

```
public class Solution {
    public String reverseString(String s) {
        char chs[] = s.toCharArray();
        StringBuilder stringBuilder = new StringBuilder();
        
        for(int i = chs.length - 1; i >=0 ; i--){
            stringBuilder.append(chs[i]);
        }
        
        return stringBuilder.toString();
    }
}
```

上面虽然 accept 了，但是会出现一些问题：

1. s没有验证
2. 已经有了 chs 数组，那么就可以在该数组上进行反正，而不用 重新再创建数组，节省空间。 `StringBuilder stringBuilder = new StringBuilder();` 本质上来说是创建了一个长度为 16的数组。

# 改良后的算法

```
public class Solution {
    public String reverseString(String s) {
        if (s == null) {
            return null;
        } else {
            char chs[] = s.toCharArray();

            int begin = 0;
            int end = chs.length - 1;

            while(end >= begin){
                char flag = chs[begin];
                chs[begin] = chs[end];
                chs[end] = flag;
                begin++;
                end--;
            }

            return new String(chs);
        }
    }
}
```

总结：1. 服务器端无论如何都需要做参数验证。2. 尽量看看节省内存



