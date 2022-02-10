<img width="628" alt="Screen Shot 2022-02-10 at 2 45 06 PM" src="https://user-images.githubusercontent.com/59748598/153509349-b4272c91-4f23-493b-ad38-d265b377fec5.png">

其实题目已经给的有点明显了只不过我傻逼看不出来，

<img width="773" alt="Screen Shot 2022-02-10 at 2 46 04 PM" src="https://user-images.githubusercontent.com/59748598/153509482-72772f03-0041-48ff-9e44-db80271b9b3f.png">

把每一个的root的结果看成root，一个个加上去

比如说n=3，按照题目给的先加root==1的时候left=dp[2]=2;right=dp[1]=1一共2*1种；  

root==2的时候左边一种右边一种一共就一种，left=right=dp[1]=1; 1*1=1种

root==3的时候左边两种右边一种left=dp[2]=2,right=dp[1]=1 left*right=2'

2+1+2=5

 
```` 
class Solution {
    
    public int numTrees(int n) {
        
        int[] dp=new int[n+1];
        dp[0]=1;//维持状态转移方程
        //dp[1]=1;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=i;j++){
                int left=dp[j-1];
                int right=dp[i-j];
                dp[i]+=left*right;
            }
        }
        return dp[n];  
    }  
}
````




