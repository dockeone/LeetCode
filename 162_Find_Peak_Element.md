# 题目

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.


# 思路

***题目的意思：***一个 peak element 就是指这个元素比它相邻的元素都要大。给定一个数组，其中 `num[i] ≠ num[i+1]`，需要找到这个 peak element，并且返回它的坐标。一个数组可能会有很多个，那么就返回其中一个都 ok。另外，假定 ` num[-1] = num[n] = -∞`。

例如：`[1, 2, 3, 1]` 的 peak element 就是 3，那么就应该返回索引 2。

***思路：***第一个思路马上就想到那就分 左，中，右三个数，那么需要注意这次的中和右的比较，其实就是下一次的左和中的比较，需要复用这个。

# 实现代码

```
public class Solution {
    public int findPeakElement(int[] nums) {
        if((nums.length == 1) || (nums[1] < nums[0])){
            return 0;
        }

        boolean nextLeftGreaterThanMiddle = nums[1] > nums[0];
        for(int i = 1; i < nums.length - 1; ++i){
            if(nums[i] > nums[i + 1]){
                if(nextLeftGreaterThanMiddle == true){
                    return  i;
                }
                nextLeftGreaterThanMiddle = false;
            } else if(nums[i] == nums[i + 1]){
                nextLeftGreaterThanMiddle = false;
            } else {
                nextLeftGreaterThanMiddle = true;
            }
        }

        return nums.length - 1;
    }
}
```

# 解决方法第二种

发现上述我这种实现需要 O(n)的时间复杂度，但是其实也可以找到最大值，那么最大值其实肯定就是 peak element了。这样时间复杂度还是 O(nlgn)。那么实现可以如下：

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        
        int flag_nums[] = nums.clone();
        
        quickSort(flag_nums,0,flag_nums.length - 1);
        
        
        return findPeakElement0(nums,flag_nums[flag_nums.length - 1]);
    }
    
    private int findPeakElement0(final int[] nums,final int target) {
        for(int i = 0 ; i < nums.length; ++i){
            if(nums[i] == target){
                return i;
            }
        }
        
        return -1;
    }
    
    private  void quickSort(int[] nums,final int start,final int end) {
        int i = start;
        int j = end;
        int pivot = getPivot(nums,start,end);
        int flag = nums[pivot];
        nums[pivot] = nums[0];

        while (i < j){
            while( (i < j) && (nums[j] >= flag) ){
                j--;
            }
            nums[i] = nums[j];

            while ( (i < j) && (nums[i] <= flag) ){
                i++;
            }
            nums[j] = nums[i];
        }
        nums[i] = flag;

        if( (i - start) > 1) quickSort(nums, start,i - 1);
        if( (end - i) > 1) quickSort(nums,i + 1,end);
    }
    
    private  int getPivot(final int[] nums,final int start,final int end) {
        int s = nums[start];
        int m = nums[(start + end) / 2];
        int e = nums[end];

        if((s >= m) && (s >= e)){
            return m >= e ? e : m;
        }
        if((m >= s) && (m >= e)){
            return s >= e ? e : s;
        }
        if((e >= s) && (e >= m)){
            return s >= m ? m : s;
        }
        return -1;
    }
}
```

# Top solution

看了一下 top solution，发现只需要 O(lgn) 的时间复杂度，效率更高。这个方法一开始还是不能理解，不过作图出来就好理解多了，参考：[[leetcode] 162 Find Peak Element(二分)](http://blog.csdn.net/nk_test/article/details/49926229)：

> 首先我们找到中间节点mid，如果大于两边返回当前的index就可以了，如果左边的节点比mid大，那么我们可以继续在左半区间查找，这里面一定存在一个peak，为什么这么说呢？假设此时的区间范围为[0,mid-1]，因为num[mid-1]一定大于num[mid]，如果num[mid-2]<=num[mid-1]，那么num[mid-1]就是一个peak。如果num[mid-2]>num[mid-1]，那么我们就继续在[0,mid-2]区间查找，因为num[-1]为负无穷，所以我们最终绝对能在左半区间找到一个peak。同理右半区间一样。

也就是说，当我们确定了 左边的节点比mid大，那么就继续在左半区间查找，因为如果此时 num[mid-2]<=num[mid-1]，那么num[mid-1]就是一个peak。如下：

![1621](http://7xrzlm.com1.z0.glb.clouddn.com/1621.png?imageMogr2/thumbnail/!35p)

如果num[mid-2]>num[mid-1]，那么我们就继续在[0,mid-2]区间查找，如下:

![1622](http://7xrzlm.com1.z0.glb.clouddn.com/1622.png?imageMogr2/thumbnail/!35p)

这个时候，你会发现，mid - 2 其实就是 mid - 1 了，此时就是一个递归循环了。

那么这么循环下去，能否确定左侧肯定有一个小一点的？ 肯定可以，因为题目说了 num[-1] = num[n] = -∞。

所有就有了此时的二分法。参考上述的网址：

```
class Solution {  
public:  
    int findPeakElement(vector<int>& nums) {  
        int left=0,right=nums.size()-1;  
          
        while(left<right)  
        {  
           int mid1=(left+right)/2;  
           int mid2=mid1+1;  
           if(nums[mid1]<nums[mid2])  
           left=mid2;  
           else  
           right=mid1;  
        }   
        return left;  
    }  
};  
```





