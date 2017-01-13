# 题目

Given an integer, write a function to determine if it is a power of two.

# 思路

在昨天看了 the power of three，那么此题的解法就可以参照它。首先求得 2^n = Integer.MAX_VALUE ，n = 1073741824， 那么 就可以 通过取余的方式得到结果。

# 解决办法

```
public class Solution {
    public boolean isPowerOfTwo(int n) {
        return (n > 0) && (1073741824 % n == 0);
    }
}
```

# Top Solution

看了别人的解决方法，主要可以利用 2^n = 10000... ，2^n - 1 = 0111111，那么两者做一个 & 操作就变成了 0000...。如下：

```
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n<=0) return false;
        return !(n&(n-1));
    }
};
```

遇到这种特殊的 2^n ，可以考虑位运算。