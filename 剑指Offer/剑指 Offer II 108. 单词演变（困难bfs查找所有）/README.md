https://leetcode-cn.com/problems/om3reC/

<img width="539" alt="Screen Shot 2022-04-02 at 1 32 43 PM" src="https://user-images.githubusercontent.com/59748598/161400247-22f5a3f2-c582-4a53-bb50-b24ee29d211e.png">

有一个方法吧所有下一次可以出现的都找出来（26个字母来回换），双层for loop

借鉴了bfs每一层把上一层所有的都清除掉的思路，来解决比如说题目这个下一层找到hot，到底是选用dot还是lot，实际上dot和lot是一层，往下走dog（来源dot），log来源于dog或者lot也算是一层，
每走一层step++

这里就需要visited set了，不然log走两次，有一个注意的，不要用==对比string，用equals，不然bug，因为从nextString方法来的是convert char array变过来的，不是=的时候从敞亮吃池子调过来的

![image](https://user-images.githubusercontent.com/59748598/161400333-9649e40c-0f12-4a3f-a3c1-c8d179532821.png)

代码：
```` 
class Solution {
    // Set<String> words;
    // Set<String> visited;
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> words=new HashSet<>();
        Set<String> visited=new HashSet<>();
        words.addAll(wordList);

        if(!words.contains(endWord)){
            return 0;
        }

        if(beginWord==endWord){
            return 1;
        }

        int step=0;
        Queue<String> queue=new LinkedList<>();
        queue.offer(beginWord);
        
        visited.add(beginWord);

        while(!queue.isEmpty()){
            int size=queue.size();
            
            step++;
            
            for(int i=0;i<size;i++){
                String cur=queue.poll();
                for(String temp : nextString(cur,words,visited)){
                    if(temp.equals(endWord)){
                        return step+1;
                    }
                    else{
                        queue.offer(temp);
                        visited.add(temp);
                    }
                }
            }
        }

        return 0;

        
    }

    public List<String> nextString(String cur,Set<String> words, Set<String> visited){
        List<String> res=new ArrayList<>();
        char[] ch=cur.toCharArray();
        String s=null;
        for(int i=0;i<cur.length();i++){
            for(char c='a';c<='z';c++){
                char temp=ch[i];
                ch[i]=c;
                s=String.valueOf(ch);
                if(words.contains(s) && !visited.contains(s)){
                    res.add(s);
                }
                ch[i]=temp;
            }
        }
        return res;
    }
}
````




