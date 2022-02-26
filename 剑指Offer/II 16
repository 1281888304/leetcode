https://leetcode-cn.com/problems/wtcaE1/

剑指offer II 16也是一样的

上面是base case，start移动到下一个

下面是特殊的case，start已经一栋楼就没必要移动

当然也可以通过set存起来，遇到duplicate就不停的从left删除删除到没有为止，判断set size，就是我在leetcode的做法


![image](https://user-images.githubusercontent.com/59748598/155820589-029a21e7-3821-4ff9-a53d-b6cbc456bcb1.png)


```` 
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s.length()<1 || s==null) return 0;
        //key character | value: last index
        HashMap<Character,Integer> map=new HashMap<>();
        int max=0;
        int start=0;
        for(int i=0;i<s.length();i++){
            char c=s.charAt(i);
            if(!map.containsKey(c)){
                // max++;
                max=Math.max(max,i-start+1);
                map.put(c,i);
                continue;
            }
            //now contains
            int temp=map.get(c)+1;
            if(temp<start){
                start=start;
            }else{
                start=temp;
            }
            max=Math.max(max,i-start+1);
            map.put(c,i);
        }

        return max;
    }
}
````

