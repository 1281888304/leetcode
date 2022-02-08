硬币可以重复使用，尝试1d 数组

<img width="532" alt="Screen Shot 2022-02-08 at 12 52 11 PM" src="https://user-images.githubusercontent.com/59748598/153073620-31ddf01c-ede7-4c46-841b-2f43745735f4.png">


注意因为不旅游天数无所谓不用买票，所以target不再days里的话直接dp[i]=dp[i-1]

也需要考虑如果第七天和第十五天最便宜（反常数据lol），所以每次比最小的时候，要把0+costs[1] cost[2] 之类的也放上去，现实逻辑：一天3块钱，7天1块，那么dp从0到7都是1块


```` 
class Solution {
    public int mincostTickets(int[] days, int[] costs) {
        Arrays.sort(days);
        int lastDay=days[days.length-1];
        //从0开始，就好比如[0,20]
        int[] dp=new int[lastDay+1];
        Arrays.fill(dp,Integer.MAX_VALUE);
        dp[0]=0;
        
        int index=0;//用来看这天有没有在days数组出现过
        for(int i=1;i<=lastDay;i++){
            //没出现过就直接跳过，不需要买票
            if(i!=days[index]){
                dp[i]=dp[i-1];
                System.out.print(" "+dp[i]);
                continue;
            }
            
            //一共就三个,直接三个一起找最小的，注意七天可能比两天便宜，15天也可能是最便宜的
            dp[i] = Math.min((i >= 1 ? dp[i - 1] : 0) + costs[0], 
                        Math.min((i >= 7 ? dp[i - 7] : 0) + costs[1], 
                                (i >= 30 ? dp[i - 30] : 0) + costs[2]));
            
            index++;
            System.out.print(" "+dp[i]);
            
        }
        return dp[lastDay];
        
    }
}


//硬币重复使用1d array
````



