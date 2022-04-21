```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 如果该单词是否存在于网格中，返回true,否则返回false
     * @param board char字符型二维数组 二维网格
     * @param word string字符串 单词
     * @return bool布尔型
     */
    public boolean exist (char[][] board, String word) {
        //dfs word search
        if(board==null || board.length<1 || word ==null || word.length()<1){
            return false;
        }
        int m=board.length;
        int n=board[0].length;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(board[i][j]==word.charAt(0)){
                    if(dfs(board,0,i,j,word))
                        return true;
                }
            }
        }
        return false;
        
    }
    
    public boolean search(int i,int j,int index,String word,char[][] board){
        if(index==word.length()){
            return true;
        }
        if(i<0 || j<0 || i>=board.length || j>=board[0].length){
            return false;
        }
        if(board[i][j]!=word.charAt(index)){
            return false;
        }
        //now success search this word, try to find next
        
        char temp=board[i][j];
        board[i][j]='%';
        boolean res= search(i+1,j,index+1,word,board) ||
        search(i-1,j,index+1,word,board) ||
        search(i,j+1,index+1,word,board) ||
        search(i,j-1,index+1,word,board);
        board[i][j]=temp;
        return res;
    }
    
    private boolean dfs(char[][] board,int index,int i,int j,String word){
        if(index==word.length()) return true;
        //consider outside of range because we need go up/down/left/right
        if(i<0 || i>=board.length || j<0 || j>=board[0].length) return false;
        //consider if word not match and returen
        if(board[i][j]!=word.charAt(index)) return false;
        //if word is match
        
        //mark it as readed
        char temp=board[i][j];
        board[i][j]='$';
        //go up/down/left/right
        boolean found=dfs(board,index+1,i-1,j,word)//up
                || dfs(board,index+1,i+1,j,word) //down
                || dfs(board,index+1,i,j-1,word)//left
                || dfs(board,index+1,i,j+1,word); //right
        board[i][j]=temp;
        return found;
       
    }
    
    
    
    
    
    
}
````
