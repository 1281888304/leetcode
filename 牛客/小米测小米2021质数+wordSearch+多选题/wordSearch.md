leetcode 79原题，我有一点没考虑到就是往下一步（上下左右）搜索的时候要更换掉搜索过的数字，不然下面的图BFB的话也能搜索到先搜索B在搜索F再回来搜索已经搜索过的B


<img width="662" alt="Screen Shot 2022-04-21 at 10 48 54 AM" src="https://user-images.githubusercontent.com/59748598/164520385-ab966377-1b73-45ec-9f39-bc775f9c1f93.png">

但是leetcode答案放上去还是超时+9/10

```` 
class Solution {
    public boolean exist(char[][] board, String word) {
        for(int i=0;i<board.length;i++){
            for(int j=0;j<board[0].length;j++){
                if(board[i][j]==word.charAt(0)){
                    if(dfs(board,0,i,j,word)){
                        return true;
                    }
                }
            }
        }
        return false;
    }
    //index is the word's char index
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
