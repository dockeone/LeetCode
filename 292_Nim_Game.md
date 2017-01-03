# Question

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

**Hint:**

If there are 5 stones in the heap, could you figure out a way to remove the stones such that you will always be the winner?

**Credits:**

Special thanks to @jianchao.li.fighter for adding this problem and creating all test cases.

Subscribe to see which companies asked this question

# My Thought

***题目的意思是：***你和你一个朋友玩游戏，有一堆石头，每次拿 1个或者2个或者3个，你拿或者你朋友拿，假如这次是你拿了，下次就是你朋友拿，假如这次你朋友拿了，下次就是你拿，这样轮流着。谁拿最后一个谁就赢了。要你写一个函数，对于给定的石头，判断你能不能赢。

***思路：***首先感觉像一个数学问题，那么首先就举例看看有没有规律：

1. 假设有 1，2，3 个的情况，我都能赢。因为一个能拿 1-3个。
2. 假设有4个。我肯定输，因为我拿1个，剩3个，对手全拿，对手赢了。我拿2个，剩2个，对手也全拿，对手也赢了，以此类推。
3. 假设有5个。由于我知道，假如剩4个，谁先手，那么谁就输。所以我要构造剩4个的情况给对手。所以我想赢就只能拿1个，那么剩4个，让对手选择，无论对手选择多少个，我都全拿，我就赢了。
4. 假设有6个。同5个的道理，我要拿2个，构造剩下4个的情况给对手。
5. 假设有7个。同上。
6. 假设有8个。这个情况下，由于我只能拿1到3个，所以我没有办法构造4个。但是好像无论我拿多少个，对手能构造4个给我，所以，被反杀，在下输了。
7. 假设有9个。突然发现剩8个的时候，先手必输，那既然我构造不了 4个，那我可以构造8个，所以这种情况下我拿1个。我赢了。
8. 假设有10个。同理，构造剩8个的情况给他。
9. 假设有11个。同理，构造剩8个的情况给他。
10. 假设有12个。发现构造不了8个，同假设有8个的那种情况一样，被反杀，我输了。

这个时候，可以稍微发现规律了。4的倍数我必输，为什么呢，因为无论我拿多少个，1-3，对手都可以构造剩下4个给我选。剩下4个，我又拿不了全部，但是至少拿1个，我拿了一个，就剩1到3个，对手都可以赢了。

但是，如果不是4个倍数的话，让我先手，我就可以构造4个倍数个给对手，对手就会陷入到上面的这个困境中，那么我就可以赢了。



# My Solution

```
package com.test;

public class Solution {
    public boolean canWinNim(int n) {
        if( n == 1 || n == 2 || n == 3) return true;
        return n % 4 == 0 ? false : true;
    }
}	
```


## Discuss Online

好像上面我的 solution还是啰嗦，囧... n==1 || n==2 || n==3 其实就是 n%4 != 0 嘛...
修改后是如下：

```
public boolean canWinNim(int n) {    
    return n % 4 != 0 ;
}
```

