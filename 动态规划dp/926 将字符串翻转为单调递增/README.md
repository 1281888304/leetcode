剑指offerII 92
https://leetcode.com/problems/flip-string-to-monotone-increasing/

<img width="538" alt="Screen Shot 2022-03-06 at 9 43 23 PM" src="https://user-images.githubusercontent.com/59748598/156974922-9bec8a59-8035-4394-881b-1ba2552a83ca.png">

动态规划，找出所有1的数量，然后每次遇到0都要判断一下（没遇到1之前的0都不用判断，不过math.min两个0都是0）

每次遇到1就++，遇到0（1之后）就判断是翻转所有的1还是把目前这个0反转了res=Math.min(one,res+1);

之后也一样


''''
class Solution {
    public int minFlipsMonoIncr(String s) {
        int res=0,len=s.length();
        int one=0;
        for(int i=0;i<len;i++){
            if(s.charAt(i)=='1'){
                one++;
            }
            else{
                res=Math.min(one,res+1);
            }
            
        }
        return res;
    }
}
''''




