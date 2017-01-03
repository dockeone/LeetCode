# Question

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.

***Credits:***

Special thanks to @jianchao.li.fighter for adding this problem and creating all test cases.

# My Thought

***题目意思：*** Ugly number 是一些正数，并且，满足 2^x * 3^y * 5^z，其中 x，y，z 为自然数。然后需要写一个算法，求一个数是不是Ugly number。

***思路：***这道题不是特别的困难，我们只需要3个 while循环，分别对2，3，5进行处理即可，给定一个数，不断的 除2，直到除不了为止，然后3，5同理，如下 Mysql Solution1。 


# My Solution

```
if(num == 1 || num == 2 || num == 3 || num == 5){
	return true;
} else if(num == 0){
	return false;
} else {

	//consider 2
    while(num % 2 == 0 ){
    	num = num / 2;
        if(num % 2 != 0) break;
        if(num == 2) return true;
    }
    
    //consider 3
    while(num % 3 == 0 ){
    	if(num == 3) return true;
       	num = num / 3;
        if(num % 3 != 0) break;
    }
    
    //consider 5
    while(num % 5 == 0 ){
    	if(num == 5) return true;
        num = num / 5;
        if(num % 5 != 0) break;
    }
    return false;
}
```

# Discuss Online

```
for (int i=2; i<6 && num>0; i++)
    while (num % i == 0)
        num /= i;
return num == 1;
```

#Summary

网上Discuss的思路和自己写的这个基本一样。但是牺牲了一些可读性。各种好坏。


