这道题是经典的不用for loop，因为不需要重复从后往前加，也不需要for loop顺序顺上去加，他是那种需要从头撸到尾的这种，大部分都不需要，leetcode784字母大小写那个也是，答案需要从头撸到尾

像leetcode46全排列就属于需要从后往前加[1,2,3]答案需要[3,2,1] / [2,1,3]

或者说leetcode 78需要从中间开始单个的这种

他的策略就是很简单，既然ip地址是四个字段，然后每个字段最多可以有三位，最大是255，就当作三道题

第一道题是每次放一个，第二道题是每次放两个，第三道题是每次放三个，一个bt方法里面先尝试着往里面放一个，再尝试放两个，再尝试放三个，每次都是不行的话就撤销指令

记得两个或者三个不可以开头是0，然后三个要小于255，还有index如果超越边界了也要停止

```` 
//能分成四份就可以了，不用在意前面那个大小
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res=new ArrayList<>();
        if(s.length()>12) return res;
        StringBuilder sb=new StringBuilder();
        bt(res,sb,0,s,0);
        return res;
    }
    //不用for loop因为不用重复使用
    private void bt(List<String> res,StringBuilder sb,int index,String s,int part){
        if(index==s.length() && part==4){
            StringBuilder tempRes=new StringBuilder(sb);
            tempRes.deleteCharAt(0);//删除第一个"."
            res.add(tempRes.toString());
            return;
        }
        //从0开始最多只能由四段，4的话意味着五段了
        if(part>=4){
            return;
        }
        //index超过了范围了
        if(index==s.length()){
            return;
        }
        //放一个数字
        sb.append(".");
        sb.append(s.charAt(index));
        bt(res,sb,index+1,s,part+1);
        //撤销操作
        sb.setLength(sb.length()-2);

        //放两个数字
        //part是1第二段开始不能start from 0,返回上一步进行别的选择
        if(s.length()-index<2){
            return;
        }
        if(part>=0 && s.charAt(index)=='0'){
            return;
        }
        sb.append(".");
        sb.append(s.substring(index,index+2));
        bt(res,sb,index+2,s,part+1);
        sb.setLength(sb.length()-3);

        //放三个数字 
        //必须小于等于255
        if(s.length()-index<3){
            return;
        }
        if(part>=0 && s.charAt(index)=='0'){
            return;
        }
        int temp=Integer.parseInt(s.substring(index,index+3));
        if(temp>255){
            return;
        }
        sb.append(".");
        sb.append(temp);
        bt(res,sb,index+3,s,part+1);
        sb.setLength(sb.length()-4);

    }
}
````



