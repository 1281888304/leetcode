![Screen Shot 2022-02-07 at 10 04 55 AM](https://user-images.githubusercontent.com/59748598/152846001-24efb10a-19f2-4dc9-8a35-89ef2366f95b.png)

这种每次往背包放一个或者拿出来 ，类似于每层只能投一次币，就是没层只能玩一次，dp背包二维数组

背包问题都要处理target，这里的target因为有负数，所以是[-sum,sum]

![Screen Shot 2022-02-07 at 10 06 46 AM](https://user-images.githubusercontent.com/59748598/152846261-c0efe56b-5a5f-49d5-93ec-a69a74978396.png)

第一行的两个比如 0+1 0-1各有一个,要注意如果是nums[0]=0那么0就是2

然后这里为了方便写，我们的j就是[-sum,sum] for(int j=0sum;j<=sum;j++)

然后底层逻辑是上一行有的就+/- 出来了我们的状态方程dp[i][j+sum]:dp[i-1][j-num+sum] + dp[i-1][j+num+sum]。（上一行加和减顺序不要搞错了）

dp[i-1][j-num+sum]是上一行不为0的，加上这一行的num 

dp[i-1][j+num+sum] 是上一行不为0的，减去这一行的num

但是要注意边界，比如说j-num<-sum就比如target是-5（第一列），在这一列左上没有不能➕

                j-num>-sum就比如target是-5（第一列），在这一列右上没有不能➖ 
```` 
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum=0;
        int n=nums.length;
        
        for(int i=0;i<n;i++)
            sum+=nums[i];
        
        //题目乱给target
        if(Math.abs(target)>sum) return 0;
        
        int[][] dp=new int[n][sum*2+1];
        
        dp[0][sum + nums[0]] += 1;
	    dp[0][sum - nums[0]] += 1; //确保第一行有0，+0 -0重复了
        
        for(int i=1;i<n;i++){
            int num=nums[i];
            for(int j=-sum;j<=sum;j++){
                //左边边界问题，如果这样的话，找不到+，只可以-
                if(j-num<-sum){
                    dp[i][j+sum]=dp[i-1][j+num+sum];
                }
                else if(j+num>sum){
                    dp[i][j+sum]=dp[i-1][j-num+sum];
                }
                else{
                    dp[i][j+sum]=dp[i-1][j+num+sum]+dp[i-1][j-num+sum];
                }
            }
        }
        
        return dp[n-1][sum+target];
    }
}
//底层逻辑是上一层的两个，一个+一个-，比如第结果行就是取决于nums[3]行的target=2 的4 加上上一行target =4 的1； 4+1=5
````



