# Question

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.


#Thought

***题目意思：*** 给定一个int型非负数组，然后再加一返回，例如：

1. digits[] = {9,9} ，那么返回 [1,0,0]；
2. digits[] = {1,9,9} ，那么返回 [2,0,0]；
3. digits[] = {9,1,9} ，那么返回 [9,2,0]；
4. digits[] = {1,2,3} ，那么返回 [1,2,4]；

***解决思路：*** 这个题 关键在于 9 ，如果没有 9 的话，那么 加一 则直接再最后一位加一 即可。假如有 9 的情况下 ，需要进一位。此时其实还是可以利用 一个 赛跑的思路，一个变量往前探测，遇到9，那么后面的变量就等于它，表明，这里有可能是要进位的。

# Solution

```
public class Solution {
    public int[] plusOne(int[] digits) {
        
        int front = 0;
        int back = -1;
        
        for(; front < digits.length; ++front){
            if(digits[front] != 9){
                back = front;
            }
        }
        if(digits[front - 1] == 9){
            if(back == -1){
                int newDigits[] = new int[digits.length + 1];
                newDigits[0] = 1;
                for(int i = 1; i < digits.length + 1; ++i){
                    newDigits[i] = 0;
                }
                return newDigits;
            }
            digits[back] = digits[back] + 1;
            back++;
            for(; back < front; ++back){
                digits[back] = 0;
            }
        } else {
            digits[front - 1] = digits[front - 1] + 1;
        }
        
        return digits;
    }
}
```