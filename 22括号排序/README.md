这道题就是括号来括号关的，特殊的题，就有一个open的int和close的int

先判断open，因为他要按顺序排放，所以说你先判断open的，如果open<max，那么就往里面加

这时候比如说加到三个了"((("就往下走判断close，close就不能小于max了，因为一个open对应一个close，所以说，这里的情况是如果close小于open的情况，就往里添加

得到第一个"((()))"然后上面撤销，当然下面也要撤销，这样才能不同的答案

```` 
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list=new ArrayList<>();
        backTracking(list,new StringBuilder(),0,0,n);
        return list;
    }
    
    private void backTracking(List<String> list,StringBuilder current,int open,
                             int close,int max){
        //出口
        if(current.length()==max*2){
            list.add(current.toString());
            return;
        }
        if(open<max){
            current.append("(");
            backTracking(list,current,open+1,close,max);
            //撤销操作
            current.deleteCharAt(current.length()-1);
        }
        if(close<open){
            current.append(")");
            backTracking(list,current,open,close+1,max);
            //撤销操作
            current.deleteCharAt(current.length()-1);
            
        }
    }
}
````




