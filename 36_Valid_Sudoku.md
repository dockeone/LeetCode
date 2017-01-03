# Question

Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'` .

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.

***Note:***

A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

# Thought

***题目意思：***就是给定表示这个表的二维数组，然后判断是不是一个数独，也就是平常玩的九宫格游戏。那么可以输入 字符`'.'`，也按照数独规则判断即可。Ps：之前一直没搞明白输入 `'.'`是什么意思。总之就是横竖，方块区域不同即可。

***思路：***一想到的思路就是 平常是怎么玩的，那么就怎么实现。平常一般我们判断符不符合九宫格，数独，就是横着看一遍，再竖着看一遍，最后在区域看一遍，时间复杂度为 O(n^2).如下为实现：

# Solution

```
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        return rowCheck(board) && colCheck(board) && blockCheck(board);
    }
    
    public boolean rowCheck(char[][] board){
        for(int i = 0 ; i < board[0].length; ++ i){
            ArrayList hsc = new ArrayList();
            for(int j = 0 ; j < board[0].length; ++j){
                if('.' == board[i][j]){
                    hsc.add(board[i][j]);
                } else if (!hsc.contains(board[i][j])){
                    hsc.add(board[i][j]);
                }
            }
            
            if(hsc.size() != board[0].length){
                return false;
            }
        }
        return true;
    }
    
    public boolean colCheck(char[][] board){
        for(int i = 0 ; i < board[0].length; ++ i){
            ArrayList hsc = new ArrayList();
            for(int j = 0 ; j < board[0].length; ++j){
                if('.' == board[j][i]){
                    hsc.add(board[j][i]);
                } else if(!hsc.contains(board[j][i])){
                    hsc.add(board[j][i]);
                }
            }
            if(hsc.size() != board[0].length){
                return false;
            }
        }
        
        return true;
    }
    
    public boolean blockCheck(char[][] board){
        for(int i = 0 ; i < board[0].length; i = i + 3){
            for(int j = 0 ; j < board[0].length; j = j + 3){
                boolean flag = blockCheck0(board,i,j);
                if(flag == false){
                    return false;
                }
            }
        }
        return true;
    }
    
    public boolean blockCheck0(char[][] board,int rowBegin,int colBegin){
        ArrayList hsc = new ArrayList();
        for(int i = rowBegin ; i < rowBegin + 3; ++i){
            for(int j = colBegin ; j < colBegin + 3; ++j){
                if('.' == board[i][j]){
                    hsc.add(board[i][j]);
                } else if(!hsc.contains(board[i][j])){
                    hsc.add(board[i][j]);
                }
            }
        }
        if(hsc.size() != board[0].length){
            return false;
        } else {
            return true;
        }
    }
}
```

# Discuss Online

Ps：网上的一些比较 hot 的答案也是 O(n^2) 的时间复杂度。