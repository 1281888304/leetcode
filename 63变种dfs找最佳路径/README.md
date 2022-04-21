牛客vivo变换尝试而已，其实这种不用往左和上的没必要，就是(m-1)X(n-1),写来玩一下，可以看到，3X3最后答案是4，（3-1）*（3-1）

<img width="1260" alt="Screen Shot 2022-04-20 at 5 20 12 PM" src="https://user-images.githubusercontent.com/59748598/164345197-2dd7f5c5-c723-4d2e-8b9a-8650e4dc5ab0.png">

代码：
```` 
class Solution {
    int endX,endY;
    int[][] dp;
    
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        endX=obstacleGrid.length;
        endY=obstacleGrid[0].length;
        dp=new int[endX][endY];
        dfs(0,0,endX-1,endY-1,0,obstacleGrid);
        return dp[endX-1][endY-1];
    }
    
    public void dfs(int x,int y,int endX,int endY,int count,int[][] obstacleGrid){
        if(x<0 || y<0 || x>endX || y >endY){
            return;
        }
        if(obstacleGrid[x][y]==1){
            return;
        }
        //核心，比新来的小就不考虑了
        if(dp[x][y]!=0 && dp[x][y]<count){
            return;
        }
        
        dp[x][y]=count;
        
        if(x==endX && y==endY){
            return;
        }
        count++;
        dfs(x+1,y,endX,endY,count,obstacleGrid);
        dfs(x,y+1,endX,endY,count,obstacleGrid);
        
        
    }
}
````







