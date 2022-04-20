https://www.nowcoder.com/question/next?pid=29582167&qid=1487196&tid=55585087

<img width="631" alt="Screen Shot 2022-04-20 at 9 40 19 AM" src="https://user-images.githubusercontent.com/59748598/164280668-58324763-12f9-43b4-abe0-05031f81332d.png">


这道题和某一道简单的leetcode很像，就删删除一个就写一个helper方法，当left！=right的时候，尝试删掉left或者right可不可以形成回文



这道题傻逼的地方在于如果s是回文，要删除首个字母

```` 
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        String input=scanner.next();
        String res= helper(input);
        System.out.print(res);
        
    }
    
    public static String helper(String s){
        if(s.length()<1){
            return "false";
        }
        if(ispalidrom(s)){
            return s.substring(1,s.length());
        }
        
        int i=0,j=s.length()-1;
        StringBuilder sb=new StringBuilder(s);
        while(i<j){
            if(s.charAt(i)!=s.charAt(j)){
                
                if(ispalidrom(s.substring(i,j))){
                    return sb.deleteCharAt(j).toString();
                }
                else if(ispalidrom(s.substring(i+1,j+1))){
                    return sb.deleteCharAt(i).toString();
                }
                else{
                    return "false";
                }
            }
            i++;
            j--;
        }
        return "false";
        
    }
    private static boolean ispalidrom(String s){
        
        int i=0,j=s.length()-1;
        while(i<j){
            if(s.charAt(i)!=s.charAt(j)){
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
    
    
}
````


