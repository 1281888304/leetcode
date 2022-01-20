这道题暴力套路就是，尝试删除（不添加）每一个/不删除（添加）每一个，一开始算出来是open Reminder / close Reminder哪个大于0，开括号多了还是关括号多了，看是在什么时候删除

如果是开括号多了，那就只有开括号的时候尝试删除（不添加），关括号多了同理

最后为什么要删除，如果找到答案了，就把这一步撤销，尝试其他操作，找不到答案同理

这种string的，都要判断index是否>=s.lenghth()

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


