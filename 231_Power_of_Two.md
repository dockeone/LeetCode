# Question

Given an integer, write a function to determine if it is a power of two.

# Thought

在昨天看了 the power of three，那么此题的解法就可以参照它。首先求得 2^n = Integer.MAX_VALUE ，n = 1073741824， 那么 就可以 通过取余的方式得到结果。

#Solution

```
public class Solution {
    public boolean isPowerOfTwo(int n) {
        return (n > 0) && (1073741824 % n == 0);
    }
}
```