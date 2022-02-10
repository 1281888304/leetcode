这道题就是两个字符串之间对比 ，在对比拼接的时候我们需要用到2d数组int

最长回文可以看成s 和s.reverse的对比，在删除了谁谁谁还能不能相等（下面有案例讲解）

因为这题可以正着来也可以反着，反着那个s.charAt(index)不用-1，所以就反着来，不然正着其实也一样，正着就是第一行第一列都是0 （空 vs 空）

其实不一定下往上，正常从最后一行倒着走也行

首先是default，不用设置，最后一行最后一列都是0，因为空对比空最长子回文是0（下面有更详细的解释）
![image](https://user-images.githubusercontent.com/59748598/153273970-595f17fb-a7c9-40b9-8f4d-0a95bc002456.png)

在这里刚好解释一下这个原理，相当于bb（上面）对比bab的最长子回文（允许删除） ==2 如果这个节点上面的和左边的match了，就从右下拿上来+1，因为右下代表着b对于ab最长的是1，

如果不match，让我们看看最后一列（空的左边一列）代表着b对应b最长是1，然后往上走时a，b对于ab是1，b对于bab是1 。。。。不做赘述了

![image](https://user-images.githubusercontent.com/59748598/153275118-398b0b0d-0a38-47f1-b24b-4a00da9857ba.png)

b=>ab为什么是1，因为b对于b是1，ab删除a=> b=b；把目光看到dp[3][3]为什么bb=>ab是1，因为可以从下面得知b=b=》1 或者右边b=>ab =1(b=b)，

不match的时候就可以看下面（删除左边当前）

或者看右边（删除上面当前）

match看右下角，不包括当前的字母的最长，然后+1





完整的


![image](https://user-images.githubusercontent.com/59748598/153274121-7e0d0064-833a-4228-8995-fa5f0e60527b.png)


完整代码：
```` 
class Solution {
    public int longestPalindromeSubseq(String s) {
        
        
    StringBuilder s2 = new StringBuilder(s);
    s2.reverse();
    String str2 = s2.toString();
    int[][] dp = new int[s.length()+1][str2.length()+1];
    
    for(int i = dp.length-2 ; i >= 0 ; i--)
    {
        for(int j = dp[0].length-2 ; j >= 0 ; j--)
        {
            if(s.charAt(i) == str2.charAt(j))
            {
                dp[i][j] = dp[i+1][j+1] + 1;
            }
            else
            {
                dp[i][j] = Math.max(dp[i+1][j] , dp[i][j+1]);
            }
        }
    }
    return dp[0][0];
        
    }
    
   
}
````



