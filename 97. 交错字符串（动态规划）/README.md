首先应为每次投币一次，所以2d数组，但是给了两个交错的字符串，target就不适合放在最上面了，上和左边分别为s1 s2

<img width="851" alt="Screen Shot 2022-02-09 at 9 30 58 AM" src="https://user-images.githubusercontent.com/59748598/153257018-3552f099-8eca-4c24-baf3-ae89ec26d253.png">

有几个边界条件，dp[0][0]=true当字符串是"" 的时候不投币（不做出选择）

然后选择从哪一个开始，假设都可以从两边开始

<img width="376" alt="Screen Shot 2022-02-09 at 9 33 31 AM" src="https://user-images.githubusercontent.com/59748598/153257255-e325268f-2e0d-4754-a778-02c51bbfc7ba.png">

然后我们第一行第一列有了，就开始向右（找上面的字符串）/向下（找左边字符串）

<img width="507" alt="Screen Shot 2022-02-09 at 9 34 30 AM" src="https://user-images.githubusercontent.com/59748598/153257438-e3d666b2-0a9b-4ada-8d47-c21d164a3b62.png">

这就是我们的dp动态函数

 
```` 
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1=s1.length();
        int len2=s2.length();
        int len3=s3.length();
        
        if(len3!=len1+len2)
            return false;
        
        boolean[][] dp=new boolean[len1+1][len2+1];
        dp[0][0]=true;
        //第一列default，如果从s1第一个开始能满足几个
        for(int i=1;i<len1+1;i++){
            if(s1.charAt(i-1)==s3.charAt(i-1))
                dp[i][0]=true;
            else
                break;
        }
        //第一行default，如果从s2第一个开始能满足几个
        for(int j=1;j<len2+1;j++){
            if(s2.charAt(j-1)==s3.charAt(j-1))
                dp[0][j]=true;
            else
                break;
        }
        
        for(int i=1;i<len1+1;i++){
            for(int j=1;j<len2+1;j++){
                //向下走,要前面符合。    and。   这个char也符合
                dp[i][j]=(dp[i-1][j] && s1.charAt(i-1)==s3.charAt(i+j-1)) ||
                         (dp[i][j-1] && s2.charAt(j-1)==s3.charAt(i+j-1));
                //往右走，要前面符合。   and。    这个char也符合
            }
        }
        
        return dp[len1][len2];
        
        
    }
}
````





