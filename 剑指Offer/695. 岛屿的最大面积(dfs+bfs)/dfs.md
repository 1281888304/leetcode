https://leetcode-cn.com/problems/max-area-of-island/




<img width="554" alt="Screen Shot 2022-04-06 at 12 55 53 PM" src="https://user-images.githubusercontent.com/59748598/162059990-ddf16d58-0042-4aaa-80b3-b53618f08155.png">

dfs的话就是遍历每一个，然后判断哪一个最大，一种是全局变量一种递归方法返回int

没有全局变量：
```` 
class Solution {
    
    public int maxAreaOfIsland(int[][] grid) {
        if(grid.length==0 || grid==null){
            return 0;
        }

        //遍历所有 m X n
        int m=grid.length;
        int n=grid[0].length;
        int max=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==1){
                    int temp=bt(grid,i,j,m,n);
                    max=Math.max(temp,max);
                    
                }
            }
        }
        
        return max;

    }

    private int bt(int[][] grid,int row,int col,int m,int n){
        if(row<0 || row>=m || col<0 || col>=n){
            return 0;
        }
        if(grid[row][col]!=1){
            return 0;
        }
        int res=1;
        //up down left right
        grid[row][col]=0;
        res+=bt(grid,row+1,col,m,n);
        res+=bt(grid,row-1,col,m,n);
        res+=bt(grid,row,col-1,m,n);
        res+=bt(grid,row,col+1,m,n);
        return res;
    }


}
````

全局变量垃圾方法：
```` 
class Solution {
    private int area=0, temp=0;
    public int maxAreaOfIsland(int[][] grid) {
        if(grid.length==0 || grid==null){
            return area;
        }

        //遍历所有 m X n
        int m=grid.length;
        int n=grid[0].length;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==1){
                    bt(grid,i,j,m,n);
                    
                    area=Math.max(area,temp);
                    temp=0;
                }
            }
        }
        
        return area;

    }

    private void bt(int[][] grid,int row,int col,int m,int n){
        if(row<0 || row>=m || col<0 || col>=n){
            return;
        }
        if(grid[row][col]!=1){
            return;
        }
        temp++;
        //up down left right
        grid[row][col]=0;
        bt(grid,row+1,col,m,n);
        bt(grid,row-1,col,m,n);
        bt(grid,row,col-1,m,n);
        bt(grid,row,col+1,m,n);
    }


}
````





