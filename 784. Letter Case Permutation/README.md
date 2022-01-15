<img width="622" alt="Screen Shot 2022-01-14 at 10 32 33 PM" src="https://user-images.githubusercontent.com/59748598/149611923-ea7e272e-1a76-4f03-a0cd-42afa0697854.png">


这道题就是很基本的，迷惑性让你使用for loop其实不用

因为它不需要从后往前添加，也不需要排列出所有可能

只需要先把他变成小写，然后遇到字母的时候，在下面多列变成大写的递归，就可以比如说 a1b2碰到a的时候，a1b2 搞完了，如果没有下面就回到第一层，答案直接只有a1b2

有了以后回到b  a1B在继续往后走得到a1B2（撤销了b在得到B）


class Solution {
    public List<String> letterCasePermutation(String s) {
        List<String> res=new ArrayList<>();
        s=s.toLowerCase();
        bt(s,new StringBuilder(),0,res);
        return res;
        
    }
    //重点是不需要for loop
    public void bt(String s, StringBuilder cur, int index,List<String> res){
        //出口
        if(index==s.length()){
            res.add(cur.toString());
            return;
        }
        cur.append(s.charAt(index));
        bt(s,cur,index+1,res);
        cur.deleteCharAt(cur.length()-1);
        
        if(!Character.isDigit(s.charAt(index))){
            cur.append(s.substring(index,index+1).toUpperCase());
            bt(s,cur,index+1,res);
            cur.deleteCharAt(cur.length()-1);
        }
    }
}
