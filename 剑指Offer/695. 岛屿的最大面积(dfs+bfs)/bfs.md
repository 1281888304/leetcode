https://leetcode-cn.com/problems/max-area-of-island/submissions/

<img width="574" alt="Screen Shot 2022-04-06 at 2 22 37 PM" src="https://user-images.githubusercontent.com/59748598/162073420-fba61d8b-97ff-4e47-88a7-4dcf90b7b837.png">



这个做法很慢很慢，但是jing dian 的bfs。理论就是每一个方格都看成一层（bfs就是一层一层的遍历（二叉树）），

inner for里面每次到一个格子都把这一层（一个格子看成一层）push进去，

```` 
Queue<Integer> queueRow = new LinkedList<Integer>();
                Queue<Integer> queueCol = new LinkedList<Integer>();
                queueRow.offer(i);
                queueCol.offer(j);
````


然后用while loop再去判断如果目前的方格==1，把前后左右都push进去，==0/超过边界就跳过

```` 
while(!queueRow.isEmpty()){
                    int row=queueRow.poll();
                    int col=queueCol.poll();

                    if(row<0 || row>=m || col<0 ||col>=n){
                        continue;
                    }
                    if(grid[row][col]!=1){
                        continue;
                    }
                    cur++;
                    grid[row][col]=0;
````


当然和dfs一样，判断过要把1换成0



然后利用两个int数组让他们呢吧上下左右都加进去

```` 
//用两个数组让他们呢上下左右走,类似于dfs的上下左右操作,把上下左右加到queue
                    int[] rows=new int[]{0,0,1,-1};
                    int[] cols=new int[]{1,-1,0,0};

                    for(int index=0;index<4;index++){
                        int nextRow=row+rows[index];
                        int nextCol=col+cols[index];
                        queueRow.offer(nextRow);
                        queueCol.offer(nextCol);
                    }
````

完整代码：
 
```` 
class Solution {
    public int maxAreaOfIsland(int[][] grid) {

        int res=0;
        int m=grid.length;
        int n=grid[0].length;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                //这一块的大小
                int cur=0;
                Queue<Integer> queueRow = new LinkedList<Integer>();
                Queue<Integer> queueCol = new LinkedList<Integer>();
                queueRow.offer(i);
                queueCol.offer(j);
                //如果是0/out of borner，就不行，bfs就是一层层，每一层都搞完就到下一层，这里一层看成一个空格
                while(!queueRow.isEmpty()){
                    int row=queueRow.poll();
                    int col=queueCol.poll();

                    if(row<0 || row>=m || col<0 ||col>=n){
                        continue;
                    }
                    if(grid[row][col]!=1){
                        continue;
                    }
                    cur++;
                    grid[row][col]=0;
                    //用两个数组让他们呢上下左右走,类似于dfs的上下左右操作,把上下左右加到queue
                    int[] rows=new int[]{0,0,1,-1};
                    int[] cols=new int[]{1,-1,0,0};

                    for(int index=0;index<4;index++){
                        int nextRow=row+rows[index];
                        int nextCol=col+cols[index];
                        queueRow.offer(nextRow);
                        queueCol.offer(nextCol);
                    }

                }
                res=Math.max(res,cur);
            }
        }
        return res;
    }
}
````








