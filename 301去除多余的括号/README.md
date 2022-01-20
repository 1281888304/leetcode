这道题暴力套路就是，尝试删除（不添加）每一个/不删除（添加）每一个，一开始算出来是open Reminder / close Reminder哪个大于0，开括号多了还是关括号多了，看是在什么时候删除

如果是开括号多了，那就只有开括号的时候尝试删除（不添加），关括号多了同理

最后为什么要删除，如果找到答案了，就把这一步撤销，尝试其他操作，找不到答案同理

这种string的，都要判断index是否>=s.lenghth()

```` 
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        Set<String> res=new HashSet<>();
        StringBuilder sb=new StringBuilder();
        int openRem=0,closeRem=0;
        //先算出多了多少个开括号（open）或者多了多少个关括号（close）
        for(char c : s.toCharArray()){
            if(c=='('){
                openRem++;
                
            }
            else if(c==')'){
                if(openRem>0){
                    openRem--;
                }else{
                    closeRem++;
                }
            }
        }

        bt(s,0,sb,res,0,0,openRem,closeRem);
        return new ArrayList<>(res);
    }
    /**
         * 回溯函数
         * 分别对字符串中的每一位置的字符进行处理，最终获得符合要求的字符串加入集合中
         * @param sb 储存当前处理过且未去除字符的字符串
         * @param index 当前处理的字符位置
         * @param open 当前sb中储存的左括号数
         * @param close 当前sb中储存的右括号数
         * @param openRem 当前需要去除的左括号数
         * @param closeRem 当前需要去除的右括号数
         */
    private void bt(String s,int index,StringBuilder sb,
                   Set<String> res,int open,int close,
                   int openRem,int closeRem){
        if(index==s.length()){
            if(openRem==0 && closeRem==0){
                res.add(sb.toString());
            }
        }
        if(index>=s.length()){
            return;
        }
        char c=s.charAt(index);
        //先做删除处理，删除就是不添加这个字符串
        if(c=='(' && openRem>0){
            //如果open reminder >0 删除（不添加）这个开括号
            bt(s,index+1,sb,res,open,close,openRem-1,closeRem);
        }
        else if(c==')' && closeRem>0){
            //close reminder >0 删除（不添加）这个关括号
            bt(s,index+1,sb,res,open,close,openRem,closeRem-1);
        }
       
        //下面就是不删除处
        sb.append(c);
        
        if(Character.isLetter(c)){
            //字母和本题目无关直接继续
            bt(s,index+1,sb,res,open,close,openRem,closeRem);
        }
        else if(c=='('){
            //正常的添加open
            bt(s,index+1,sb,res,open+1,close,openRem,closeRem);
        }
        else if(c==')' && open>close){
            //添加关括号，open>close必须有，不然就不符合一开一关的格式了，
            //不能大于等于，等于的话close多了一个也不行
            //这里相当于如果open<=close,就删除这个close（不添加）
            bt(s,index+1,sb,res,open,close+1,openRem,closeRem);
        }
        //撤销操作
        sb.deleteCharAt(sb.length() - 1);    
        
         
    }
}
//这道题是22题的升级版，为什么要撤销操作，因为我们平时写for loop的时候，如果添加失败或者找到答案了，就撤销掉走下一步，这里同理，如果找到答案了，那就删掉这一步操作，回去尝试着删除其他的，因为这里不是仅仅有这一个答案，很多个答案基本是都是删除


````


