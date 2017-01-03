# Question

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

**Note:**

1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

**Credits:**

Special thanks to @jianchao.li.fighter for adding this problem and creating all test cases.

Subscribe to see which companies asked this question


# My Thought
***题目的意思：*** 给一个数组，把 数组中的0放在最后，那些不是0的要保留相对位置。要求不能创建额外的数组，尽量减少操作。

***思路：***

- 第一个反应就是和插入排序有点相同。
- 其次，就是要考虑把所有的 0 沉底。就好像 JVM的垃圾回收的 复制算法一样，把需要的移动到一边，剩下的全部清除即可。
- 其三，想到的就是非零的不断往前即可，最后剩下的再补0.

第一第二种可能不太行，插入排序的话，万一遇到 0 0 0 1 ，也就是说，重复的怎么往前插，这个有点棘手。

对于第三种不断往前移动，那么每个数需要向前移动的个数可能不同，例如1，3，5 那么，第二位的就向前移动1位，第四位的就向前移动2位。不过这种方式可能可行，因为 我可以首先记录下有哪些位置有0。

再具体些就是：

- 我可以首先一个 for 循环遍历这个数组，发现 x 位置首先有1个零，然后我全局变量记录有零 1个，记录下该位置；
- 然后，再找一下0，假如在 y 位置找到了，全局变量记录有零 2个，那么 x 到 y 这段位置的数就往前移动 2-1位；
- 然后，再找一下0，假如在 z 位置找到了，全局变量记录有零 3个，那么 y 到 z 这段位置的数就往前移动 3-1位；

这样应该可行，时间复杂度还是O(n)，试试算法实现如下：

# My Solution

```
public class Solution {
    public void moveZeroes(int[] nums) {
        
        int num0 = 0;
        int setBegin = 0;
        int numBegin = 0;
        int i;
        
        for(i = 0; i < nums.length; i++){
            if(nums[i] == 0){
                num0++;
                if(num0 >= 2) moveNum(nums,setBegin,numBegin,i - numBegin);
                setBegin = i - num0 + 1;
                numBegin = i + 1;
            }
        }
        
        //关于最后一位是否为0的处理
        if( nums[i - 1] != 0) moveNum(nums,setBegin,numBegin,i - numBegin);
        
        //最后赋0
        for(i = nums.length - 1; i > nums.length - 1 - num0; i--)
            nums[i] = 0;
    }
    
    private void moveNum(int nums[],int setBegin,int numBegin,int times){
         for(int m = setBegin,k = 0; m < setBegin + times; ++m,++k){
            nums[m] = nums[numBegin + k];
        }
    }
}
```

# My Solution2

几个月前做个这道题。看了一些当时的代码，思路是这样的：还是采用插入排序的做法，把零沉到最后。不过这种算法要比 My Solution 的复杂度要高，因为它的移动有可能是多余的，实际也是很多都是多余了。 Code is：

```
public class Solution {
    public void moveZeroes(int[] nums) {
        int length = nums.length;
        
        for(int i = length - 1; i >= 0; i--){
            int j = nums[i];
            
            if((j == 0) && (i != length - 1)) {
                int k = i;
                while(true){
                    nums[k] = nums[k + 1];
                    k++;
                    if((k + 1) == length) break;
                }
                nums[length - 1] = 0;
            } else {
                ;
            }
        }
    }
}

```


# Discuss Online

看了 Discuss 的别人的做法，只能说"我靠,这也行"，贴代码：

```
public void moveZeroes(int[] nums) {
    if (nums == null || nums.length == 0) return;        

    int insertPos = 0;
    for (int num: nums) {
        if (num != 0) nums[insertPos++] = num;
    }        

    while (insertPos < nums.length) {
        nums[insertPos++] = 0;
    }
}
```

思路就是：两个人赛跑，前面跑得快的人，把非0的数扔给跑得慢的人，这样，跑得慢的人就相当于重构了这个数组...



# Summary
思路可以有3种。

- 要把 0 往后沉，自然就能想到插入排序。这是一种从后往前的想法。
- 还有一种想法就是从前往后的角度思考。
- 最后一种想法就是赛跑，利用跑得慢的人对数组进行重构。



