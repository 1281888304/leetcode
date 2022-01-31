<img width="519" alt="Screen Shot 2022-01-31 at 3 11 47 PM" src="https://user-images.githubusercontent.com/59748598/151888306-0b7ba0f0-209a-4120-a9cd-50e8fba48f2f.png">

只能有两个character字符，大概是set/map，算法逻辑是一旦有新的加进来size超过三，滑动窗口算法保证每次滑动窗口都是满足只有两个

eceba的时候，只要往set里面添加size不超过二，left不动，超过了比如说到b这里，从e开始往回找新的left，删除多的

ccaabbb到b的时候，新的left是第一个a index=2

![image](https://user-images.githubusercontent.com/59748598/151888508-65e07366-bb75-4256-a416-efe948043660.png)

```` 


class Solution{
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if(s.length()<3)
            return s.length();
        int left=0,right=0;
        Set<Character> set=new HashSet<>();
        
        int maxLen=0;
        while(right<s.length()){
            char c=s.charAt(right);
            set.add(c);
            if(set.size()>2){
                left=right-1;
                while(s.charAt(left-1)==s.charAt(left)){
                    left--;
                }
                set.remove(s.charAt(left-1));
            }
            maxLen=Math.max(maxLen,right-left+1);
            right++;            
        }
        return maxLen;
    }
}
````





