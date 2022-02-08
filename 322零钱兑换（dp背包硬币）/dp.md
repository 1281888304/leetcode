![image](https://user-images.githubusercontent.com/59748598/153043208-385cf057-6798-4cdf-a35f-973677687206.png)

图里coin[1,2,5] amount/target==11


就是画出图，每一个每一个的和之前的对比。这里的default是dp[0]=0； ： target=0的时候，我们自然也不用投币

有两种情况，第一个刚好nums[i] ==coin在我们的

还有一种情况是一个个对比，那结果来说（图下面有） 当coin==1的时候 dp[11]=dp[1]+dp[10] / coin==2 dp[11]=dp[2]+dp[9] /coin==5 dp[11]=dp[5]+dp[6]

有了这个，就稍微慢点也在50%以上，当然要考虑不能投币的情况，target==4，5就没用了
<img width="394" alt="Screen Shot 2022-02-08 at 9 37 25 AM" src="https://user-images.githubusercontent.com/59748598/153043977-935cee5e-2503-4fc5-be58-faf99a58a020.png">


后面优化成这样,因为dp[coin]=1是固定的
<img width="333" alt="Screen Shot 2022-02-08 at 9 39 18 AM" src="https://user-images.githubusercontent.com/59748598/153044311-0bbf779e-dd3b-480e-be2f-5f27283485c8.png">

```` 
class Solution {
    public int coinChange(int[] coins, int amount) {
        if(amount==0)
            return 0;
        
        int[] dp=new int[amount+1];
        
        //先设置一下，因为后期要不停的Math.min所以献给每一个设置上最大的
        Arrays.fill(dp,amount+1);
        
        dp[0]=0;//不投
        for(int i=1;i<dp.length;i++){
            int sum=i;
            for(int coin : coins){
                // if(coin==sum){
                //     dp[i]=1;
                //     break;
                // }
                // //考虑不能投币的问题
                // if(coin<sum){
                //     dp[i]=Math.min(dp[i],dp[i-coin]+dp[coin]);
                // }
                //考虑投不了币的问题
                if(i-coin>=0){
                    dp[i]=Math.min(dp[i],dp[i-coin]+1);
                }
                
            }
        }
        return dp[amount]==amount+1 ? -1 :dp[amount];
        
    }
}

//dp存着到达的最少coins

````



