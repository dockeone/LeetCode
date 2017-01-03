# Question
---

Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?

# My Thought
---

也是没解出来，感觉和之前的 HashSet 有点像，但是也弄不出。看了一些 Discuss，用得蛮巧，如下代码：

# Discuss Online
---

这个解决比较残暴：

```
public class Solution {
    public boolean isPowerOfThree(int n) {
        // 1162261467 is 3^19,  3^20 is bigger than int  
        return ( n>0 &&  1162261467%n==0);
    }
}
```

But，下面这一种解法没看懂，Mark：

```
public boolean isPowerOfThree(int n) {
    return (Math.log10(n) / Math.log10(3)) % 1 == 0;
}
```




