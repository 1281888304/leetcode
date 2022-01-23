https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/

这道题很简单，就是题目挖了坑，比如说+ 0123  0 ；    +0123=> 123

首先把前后的空格清掉，中间的不要清理，然后第一步判断正还是负，也要考虑没有正负号默认正数

Integer那里max如果刚好等于Integer.max 2147483648就返回Integer.max /min所以要考虑到8，因为有可能刚好等于

```` 
class Solution {
    public int strToInt(String str) {
        
        str=str.trim(); //去除空格
        if(str==null || str.length()<=0) return 0;
        //开始便利的节点
        int start=0;
        //正负号，+就是1 ；   负数:-1默认是1
        int sign=1;
        if(str.charAt(0) =='-'){
            start=1;//从第二位起
            sign=-1;
        }
        else if(str.charAt(0)=='+'){
            start=1;
        }
        //用来判断，因为res*10
        int max=Integer.MAX_VALUE/10;
        int res=0;
        //考虑到有很多默认没有正负号，默认为正
        for(int i=start;i<str.length();i++){
            char c=str.charAt(i);
            //不是数字
            if(c>'9' || c<'0'){
                break;
            }
            //超过Integer的承受范围
            if(res>max || (res==max && c>='8')){
                return sign==1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
            //在range 内
            res=res*10+(c-'0');
        }

        return res*sign;
        
    }
}
````



