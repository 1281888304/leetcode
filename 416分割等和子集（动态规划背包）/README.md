<img width="529" alt="Screen Shot 2022-02-06 at 12 34 37 PM" src="https://user-images.githubusercontent.com/59748598/152700291-41be2897-b127-41d8-b8e6-c7a31aa6af89.png">

我们这道题可以拆成背包问题/投币问题 （投币是我自己傻逼觉得背包单位体积和总体积在脑子里不够透彻转换的）

先得到sum（全部硬币），除二得到target，如果其中有部分硬币加在一起==target，就有答案，因为剩下的组合在一起也是target（target=sum-target）然后因为必须要整除2，所以必须是偶数
<img width="563" alt="Screen Shot 2022-02-06 at 12 42 35 PM" src="https://user-images.githubusercontent.com/59748598/152700517-a5d22862-7d7e-4c81-9817-3c9462152b0c.png">

找到最大的数字，如果最大的比target的都大[1,2,5]肯定组合失败
<img width="451" alt="Screen Shot 2022-02-06 at 12 43 25 PM" src="https://user-images.githubusercontent.com/59748598/152700537-9078d8d3-76e2-4861-8b4e-db7a496608ef.png">

然后我们选用2d的dp数组,row=nums[]/coins[] 硬币,column列是tempTarget，动态的尝试

这样为什么确保了唯一属性，每个硬币只拿一次 2d数组为什么都是唯一属性:因为看成每行投一次币或者不投币，不会造成同一枚硬币投两次

default dp：input：[1,2,3,6]

![image](https://user-images.githubusercontent.com/59748598/152700823-9217331c-3d4e-45cc-9124-fdb5618aeb5e.png)

第一列因为j==0 target=0的情况下，不投币是可以的，所以全部是true。  第一行因为只有一个币可以投，就是coin=1的时候，正好target=1 =>true

然后第二列动态
![image](https://user-images.githubusercontent.com/59748598/152700910-abc07067-e75a-44c3-985b-f1bb7ee6e143.png)


我们可以知道在可以投币的情况下两种选择： 1不投币 2投币

1不投币： dp[i][j]=dp[i-1][j] :在j（target）一样的时候，我们不投币，那么上一次（上一行）什么成功了这一次就成功，不然上一次失败这一次就失败

2投币 ： 投币dp[i][j]=dp[i-1][j-coin]; 从第二行来看，暂时target==3 ；投了3这个硬币，看看target==（3-3）的时候，上一行，是不是true，上一行target=1的时候投币成功是true，这一行投一个2也可以正好等于target => true

原理我们了解了，现在一步步走第二行： j=1的时候上面成功了，我们跟着一起不投币/不能投币（coin=2,target=1）人家需要一块钱你给两块肯定不行； j=2 j=3就是刚刚说的，堪称target-=coin；其他也一样只不过找不到=false

不能投币：背包问题/硬币问题，target小于5，5元的硬币没办法使用。 背包： 背包只能装4斤的东西，给一个十公斤的水没法装

为什么dp[nums.length-1][target]==true答案就是true： 因为有投币成功等于一半(target)，剩下的自然可以

如果在中间某一行投币成功（j==target）是true，那么其他的会顺着往下，投币或者不投币只要其中一个可以组合成功就是true

然后我们sum（全部币）是target的两倍，所以target不可能全部币都投，一旦其中几枚硬币投成了target（全部币sum的一半，那么我们就有答案了）

 
```` 
class Solution {
    public boolean canPartition(int[] nums) {
        int sum=0;
        Arrays.sort(nums);
        int max_num=nums[nums.length-1];
        for(int i=0;i<nums.length;i++){
            sum+=nums[i];
        }
        //在不重复选择的时候，恰好选中等于target的（sun/2），剩下的自然就也等于target
        //sum如果不是偶数，那么就不能被分割，比如说sum=5，总不可能有正整数相加等于2.5
        if(sum%2!=0){
            return false;
        }
        int target=sum/2;
        
        //如果最大的比一半大，那就不用找了，肯定不可能有答案比如[1,2,5]
        if(max_num>target){
            return false;
        }
        //target从0开始多一个
        boolean[][] dp=new boolean[nums.length][target+1];
        //不选任何数，而且第一列j（暂时的target）==0所以dp[][0]=true意味着当target=0的时候，不选就可以了
        //这里本来需要第一列全部是true，但是后面算法会根据上一个判断，就节省了
        dp[0][0]=true;
        //dp[0][nums[0]]=true 第一行第一列，因为row（i）只有一个，target自然等于nums[0]；在这一行，只有一个选择也只有一个target=true
        //这里同样道理，本来需要每一行的nums[i]=j的时候=true，但是后面有判断，就不管了
        dp[0][nums[0]]=true;
        //从第二行开始因为第一行default上面设置过了
        for(int i=1;i<dp.length;i++){
            int coin=nums[i]; //这一行的num
            /*
             *这里的j是temp_target
             *本来按照图片j也是从1开始的，但是为了快点，default那里没有设置第一列全是true
            */
            for(int j=0;j<dp[0].length;j++){
                //背包问题/硬币问题，target小于5，5元的硬币没办法使用
                //背包： 背包只能装4斤的东西，给一个十公斤的水没法装
                if(j<coin){
                  dp[i][j]=dp[i-1][j];
                }
                else{
                    //投币或者不投币只要其中一个可以组合成功就是true
                    dp[i][j]=dp[i-1][j] || dp[i-1][j-coin];
                }
            }
        }
        return dp[nums.length-1][target];

    }
}
//在可以投币的情况下两种选择，不投币dp[i][j]=dp[i-1][j];  投币dp[i][j]=dp[i-1][j-coin]; 从第二行来看，暂时target==3 ；投了3这个硬币，看看target==（3-3）的时候，上一行，是不是true，上一行target=1的时候投币成功是true，这一行投一个2也可以正好等于target => true

//这样为什么确保了唯一属性，每个硬币只拿一次 2d数组为什么都是唯一属性:因为看成每行投一次币或者不投币，不会造成同一枚硬币投两次

//为什么dp[nums。length-1][target]==true答案就是true： 因为有投币成功等于一半，我们可以知道在可以投币的情况下两种选择： 1不投币 2投币
            //如果在中间某一行投币成功（j==target）是true，那么其他的会顺着往下，投币或者不投币只要其中一个可以组合成功就是true
//我们sum（全部币）是target的两倍，所以target不可能全部币都投，一旦其中几枚硬币投成了target（全部币sum的一半，那么我们就有答案了）



````













