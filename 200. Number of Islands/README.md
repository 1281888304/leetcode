这道题的关键就是所有‘1’关联的算成一个，套路就是用for loop找到第一个‘1’，然后把这个相关联的全部换成其他字符比如‘A’/‘$‘

class Solution {

    //这道题关键在于找多少个小岛
    //1和旁边所有相邻的都算一个，找到后把她们从1换成0/$不能算第二次
    public int numIslands(char[][] grid) {
        int count=0;
        for(int i=0;i<grid.length;i++){
            for(int j=0;j<grid[0].length;j++){
                if(grid[i][j]=='1'){
                    count++;
                    //and use a method to find all the 1 close it
                    //and put the 1 to 0 (no need count one more time)
                    dfs(grid,i,j);
                }
            }
        }
        return count;
    }
    //find all 1 and change all to $ 
    private void dfs(char[][] grid,int i,int j){
        //check out of boundry
        if(i<0 || i>=grid.length || j<0 ||j>=grid[0].length)
            return;
        if(grid[i][j]!='1')
            return;
        //change it
        grid[i][j]='$';
        dfs(grid,i+1,j);
        dfs(grid,i-1,j);
        dfs(grid,i,j+1);
        dfs(grid,i,j-1);
    }
}



