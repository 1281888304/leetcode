这道题是200的变形，200是通过for loop找到每一个然后把相关的全部换掉在找第二个（也不一定是第二个，因为第二个很大可能被换成别的字符）
这个套路是通过第一行最后一行第一列最后一列把四个边上的‘O’和相关联的变成别的字符
然后在把里面全部不相关的全部变成‘X’

class Solution {

    //思路不能和以前一样来，从边界出发，把所有和边界相同的O变成其他字符串比如‘A’
    //然后再把里面全部O（这时剩下的就是全部不相连接的变成X）
    //最后把‘A’变成‘O’ （相连接大的需要保留的）
    public int m;
    public int n;
    public void solve(char[][] board) {
        m=board.length;
        n=board[0].length;
        //把所有关联第一列或最后一列的O变成A
        for(int i=0;i<m;i++){
            dfs(board,i,0);
            dfs(board,i,n-1);
        }
        //把所有关联第一行或者最后一行的‘O’变成‘A’
        for(int j=1;j<n-1;j++){
            dfs(board,0,j);
            dfs(board,m-1,j);
        }

        //现在如果有‘O’就变成X因为是不关联的
        //如果有‘A’就变成O因为是关联的
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(board[i][j]=='A'){
                    board[i][j]='O';
                }else{
                    board[i][j]='X';
                }
            }
        }
        
    }
    //把所有关联的O变成A
    private void dfs(char[][] board,int i,int j){
        if(i<0 || i==m || j<0 || j==n || board[i][j]!='O'){
            return;
        }

        //current board[i][j]=='O' and connect with the corner
        board[i][j]='A';
        dfs(board,i+1,j);
        dfs(board,i-1,j);
        dfs(board,i,j+1);
        dfs(board,i,j-1);
    }
}
