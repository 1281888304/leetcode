<img width="1062" alt="Screen Shot 2022-05-02 at 2 46 54 PM" src="https://user-images.githubusercontent.com/59748598/166332867-1e501217-b7fb-4938-bb43-36caf020dd9f.png">


做过原题，但是忘记了一个细节，数字的处理，以及所有都要push进stack。数字的处理很重要，不能直接integer+char

![image](https://user-images.githubusercontent.com/59748598/166333022-968d9c7a-84ff-4688-9a67-844ce85cb105.png)

全部push进去，拿出来的时候（遇到‘]’）是先复制当前的m次，顺便把之前的拿出来一起加到res里

```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param str string字符串 
     * @return string字符串
     */
    public String compress (String str) {
        // write code here
        if(str==null || str.length()<1) return null;
        LinkedList<Integer> stackNum=new LinkedList<>();
        LinkedList<String> stackStr=new LinkedList<>();
        StringBuilder res=new StringBuilder();
        int num=0;
        
        StringBuilder temp=new StringBuilder();
        for(int i=0;i<str.length();i++){
            char c=str.charAt(i);
            if(c=='['){
                stackStr.push(res.toString());
                res=new StringBuilder();
            }
            else if(c==']'){
                StringBuilder temp2=new StringBuilder();
                int n=stackNum.pop();
                for(int j=0;j<n;j++){
                    temp2.append(res);
                }
                res=new StringBuilder(stackStr.pop().toString()+temp2);
            }
            else if(c=='|'){
                stackNum.push(num);
                num=0;
            }
            else if(c>='0' && c<='9'){
                //num=num*10+c;
                num=num*10+Integer.parseInt(c+"");
            }
            else{
                res.append(c);
            }
               
            
        }
        
        return res.toString();
    }
}
````







