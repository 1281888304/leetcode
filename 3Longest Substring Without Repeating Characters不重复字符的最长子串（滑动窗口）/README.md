这道题主要用到思路是：滑动窗口

什么是滑动窗口？

其实就是一个队列,比如例题中的 abcabcbb，进入这个队列（窗口）为 abc 满足题目要求，当再进入 a，队列变成了 abca，这时候不满足要求。所以，我们要移动这个队列！

如何移动？

我们只要把队列的左边的元素移出就行了，直到满足题目要求！

一直维持这样的队列，找出队列出现最长的长度时候，求出解！

时间复杂度：O(n)O(n)

套路是保证每次loop时候[left,i]都是正确的，每次惊醒计算，经典的slide windows

map 可以放空字符，set不可以

```` 
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length()==0) return 0;
        //key character ｜ value： index索引
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max = 0;
        int left = 0;
        for(int i = 0; i < s.length(); i ++){
            if(map.containsKey(s.charAt(i))){
                //直接挪到下一位
                //abcabc在第二个a的时候，直接挪到b
                left = Math.max(left,map.get(s.charAt(i)) + 1);
            }
            //把字符放进去
            map.put(s.charAt(i),i);
            max = Math.max(max,i-left+1);
        }
        return max;
        
    }
}



````



