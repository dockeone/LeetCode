# Question

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

***Example:*** 19 is a happy number

12 + 92 = 82

82 + 22 = 68

62 + 82 = 100

12 + 02 + 02 = 1

***Credits:***

Special thanks to @mithmatt and @ts for adding this problem and creating all test cases.

# My Thought
***思路：***这个题想了半小时没想出来。主要是从顺序和逆序想。如果是顺序的话，那么假如不是快乐数字，那么岂不是会无限循环，所以应该不能从顺序来考虑。那么假如从逆序来考虑的话，最后的结果肯定是 1，10，100，1000 .... 等。那么再反推上去，1 = 1^2；10 = 1^2 + 3^2，或者 10 = 3^2 + 1^2；但是如果是三位数就感觉没法举例看规律了...

# Discuss Online
Discuss中别人的算法：

```
public boolean isHappy(int n) {
    Set<Integer> inLoop = new HashSet<Integer>();
    int squareSum,remain;
    while (inLoop.add(n)) {
        squareSum = 0;
        while (n > 0) {
            remain = n%10;
            squareSum += remain*remain;
            n /= 10;
        }
        if (squareSum == 1)
            return true;
        else
            n = squareSum;

    }
    return false;

}
```
首先是思路：还是从顺序的角度出发。也是肯定是出现死循环的问题。但是，这个循环不是 圆周率的循环，而是有规律的循环，也就是说，会重复。那么就可以用 Set 集合判断，如果重复，不能add，那么就肯定不是 happy number 了。

#Summary

举例不足。以后可以多举例看规律。其中不仅仅是正面的例子，还有负面的例子。



