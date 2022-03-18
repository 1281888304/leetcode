https://leetcode.com/problems/decode-ways/


<img width="655" alt="Screen Shot 2022-03-18 at 11 08 42 AM" src="https://user-images.githubusercontent.com/59748598/159059365-67fa7b42-0882-4dce-b829-91e686640cc4.png">

根据数字一个个解码，就用dp 1d 数组

有以下几个不同的case，一个是default dp[0]和dp[1]都是1。 //因为0个数字/1个数字都是1种排列

还要和前一个数字组合在一起一起比较，看是不是大于26 还有0的选择

这是总结图片：
![image](https://user-images.githubusercontent.com/59748598/159059791-a6b6bae9-415e-438a-977c-d8cd43563e54.png)

代码：
```` 
class Solution {
    public int numDecodings(String s) {
        int n=s.length();
        if(n<=0 ||s.charAt(0)=='0') return 0;
        int[] dp=new int[n+1];
        
        //set default,不管如何，第一个永远是1，0是额外用来计算的，经典dp
        dp[0]=1;
        dp[1]=1;
        
        for(int i=1;i<n;i++){
            char c=s.charAt(i);
            //3 含有0的情况，当前是0
            if(c=='0'){
                //不能连续两个0
                if(s.charAt(i-1)<'1' || s.charAt(i-1)>'2'){
                    return 0;
                }
                dp[i+1]=dp[i-1];
                continue;
            }
            
            //3 含有0的情况，前一个是0
            if(s.charAt(i-1)=='0'){
                dp[i+1]=dp[i];
                continue;
            }
            //1 正常情况
            int temp=Integer.parseInt(s.substring(i-1,i+1));
            if(temp>=1 && temp<=26){
                dp[i+1]=dp[i]+dp[i-1];
            }
            //2 大于26的情况
            else{
                dp[i+1]=dp[i];
            }
        }
        return dp[n];
        
    }
}
````




