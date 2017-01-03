# Question

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

***For example:***

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

***Follow up:***
Could you do it without any loop/recursion in O(1) runtime?


# My Thought

***题目的意思是：*** 给定一个数，比如 38，然后你把它的每一位拆分，比如说38可以拆成 3 和 8，然后每一位相加，3 + 8 = 11，然后再这样循环做，直到加的结果是 一位数。

***思路1：*** 题目的意思就是思路，也就是先拆分，那么我们可以用 String.valueOf()函数 弄成 String 类型，然后再 String.charAt()函数 弄成 char 类型，最后再 Integer.parseInt();函数转换成int 类型，最后相比，递归即可。

但是可以看到，这种方式用了一个 递归。递归做得不好就成了死循环，就是有栈溢出（Stackoverflow）。题目也提示可以在O(1)的时间复杂度中弄。

***思路2：（该思路暂时没办法论证这样做是对的，以后再论证）***
那么我们刚才的思路的是每位拆分，那么能不能把数字当成一个字符串，一个 for 循环算一遍呢，其实就有点想冒泡排序那样。例如：

- 992，正确的答案是9+9+2=20，2+0=2。 
- 如果我们拆分，for循环，那么 9 + 9 = 18. 那么对这个 18 此时要怎么处理呢，是让它再拆变1+8=9，还是保留，留给后面计算。
- 假设再我们再拆分，变9，然后 + 2，变11，拆分1+1=2.这个时候是能够得到正确结果。

那么，这是个偶然的结果还是定律，再随便举个例子， 389. 那么 3+8=11，1+1=2，2+9=11，1+1=2.其实正确结果是 3+8+9=20，也就是2。所以说看起来我们是可以for循环每一位，先算以前的，然后再加。
现在我们看看能不能把他抽象成一个定律，***刚才只是举举例子，只有抽象成定律才能确定是肯定能这样做的。***

相当于 按照for循环思路的基础，假设一个数 abc，求证：假设 m 是 a 和 b 计算后的最终结果，n 是 a 和 b 计算后的中间结果，那么会有 m + c = n + c。 （Ps：例如992， 9+9=18，这个18就是中间结果，在中间结果的基础上，再进行1+8=9，这个9就是最终结果）

***所以我们只需要证明 m = n吗。不。*** 这不是简单的加减法。c会对前面的m 和n 产生影响。如果你不好理解。那么你就理解下为什么 i = i + 1。 1个苹果会等于2个苹果吗。这不是简单的加减法。 例如，992. 前两位的最终结果是9+9=18，1+8=9，是9，中间结果是18.那么加上2之后，一个变成了11，一个变成了20。 1+1 = 2+0。所以说，是会产生影响的。

***那么怎么证明... 想不出了... 囧...***


# My Solution

```
public class Solution {
    public int addDigits(int num) {
        String numStr = String.valueOf(num);

        if(numStr.length() == 1){
            return Integer.valueOf(numStr);
        } else {
            int result = 0;
            for(int i = 0; i < numStr.length(); ++i){
                result += Integer.parseInt(String.valueOf(numStr.charAt(i)));
            }
            return addDigits(result);
        }
    }
}
```

# Discuss
Discuss的 思路是什么呢？

```
class Solution {
public:
    int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
};
```
WTF，这逗我的。只能说真想不出，不过wiki有：[点这里](https://en.wikipedia.org/wiki/Digital_root)




#Summary

还是按照老百姓思路解这个题吧，拆分，相加，递归。