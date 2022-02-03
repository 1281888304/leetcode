这道题的解法就是不停的移动右指针，找到一个答案以后，开始停止，去除多余的字符串

中间inner while loop会清楚多余的，比如说不是从left开始就有word，一直loop到left是在allwords里
就开始删掉最左边，下一次得到答案，继续清楚一遍多余的，因为left第二次大概率不是从allwords里开始走 

t=ABC s=ADDADBBCDDDDDDDAAADDDEC

比如这样的话我们得到第一个答案是ADDADBBC，然后left指针往右走，这个时候allWords里A是-1（减去了两次），

先把A加，allWords里A：0 ，然后去除D，然后在去除D，到了ADBBC，之后会counter+1，allWords的A变成1，找下一个A（因为BC暂时都去除了），这个时候counter=1，跳出loop

所以loop完会变成ADBBC


```` 
class Solution {
    public String minWindow(String s, String t) {
        Map<Character,Integer> allWords=new HashMap<>();
        // for(char c : s.toCharArray()){
        //     allWords.put(c,allWords.getOrDefault(c,0)+1);
        // }
        for (char c : s.toCharArray()) allWords.put(c, 0);
        for (char c : t.toCharArray()) {
            if (allWords.containsKey(c)) allWords.put(c, allWords.get(c) + 1);
            else return "";
        }
        
        int left=0,right=0;
        String res="";
        int size=Integer.MAX_VALUE;
        int counter=t.length();
        while(right<s.length()){
            char ch=s.charAt(right++);
            if(allWords.get(ch)>0){
                counter--;
            }
            allWords.put(ch,allWords.get(ch)-1);
            
            while(counter==0){
                //先判断答案
                if(size>right-left){
                    res=s.substring(left,right);
                    size=right-left;
                }
                char ch2=s.charAt(left);
                if(allWords.get(ch2)==0)
                    counter++;
                allWords.put(ch2,allWords.get(ch2)+1);
                left++;
            }
        }
        return res;
    }
}

//因为这里有一个问题，找ABC res里含有 BDBDCA，首先找到大的，就要尝试着看看在这个答案可不可以缩小，
//这就是里面那个inner while loop作用
````



