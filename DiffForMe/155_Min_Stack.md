# Question
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

# My Thought
今天（2016.3.4）太困了，昨晚没睡好，又早起，状态不太对，没搞出来....囧。 

***思路：*** 一开始考虑是以 O(1)的时间复杂度，那么就自然想到了数组。数组可以实现 push，pop，top的 O(1)，只要设置几个变量记录下首先的开始和结束位置。但是 getMin()确一直困扰着，因为涉及到排序，数组的形式基本不可能O(1)。所以一直卡着了。

***网上别人的思路：***设置新的数据结构，该数据结构中包含了自己的值以及最小值。所以说，每个这种数据结构都会有这两个记录。那么我们 push 一个元素的时候，只需要和前一个元素相比 最小值即可，如下代码。


# Discuss Online

```
class MinStack {
    static class Element
    {
        final int value;
        final int min;
        Element(final int value, final int min)
        {
            this.value = value;
            this.min = min;
        }
    }
    final Stack<Element> stack = new Stack<>();

    public void push(int x) {
        final int min = (stack.empty()) ? x : Math.min(stack.peek().min, x);
        stack.push(new Element(x, min));
    }

    public void pop()
    {
        stack.pop();
    }

    public int top()
    {
        return stack.peek().value;
    }

    public int getMin()
    {
        return stack.peek().min;
    }
}

```

#Summary

- 这个题个人感觉比较有用，能够以 O(1) 的时间复杂度实现进行 push，pop，top，其实最关键的实现了 getMin()，工作中如果需要用到栈，也需要用到求最大最小或者中间值等，那么就可以参考重写栈。
- 该题没有解出的根本原因在于思路太单一，总是从数组入手，怎么让数组的排序能达到O(1)，但是实际上可以设置新的数据结构（包含了我们要的最小值），每次push 就和上一个相比即可。
- 设置到 O(1)的时间复杂度，要么就是 数组，要么就是和上一个相比，或者和固定的一个东西相比。

