https://www.nowcoder.com/question/next?pid=29582167&qid=1487197&tid=55584041



<img width="1213" alt="Screen Shot 2022-04-20 at 11 16 55 AM" src="https://user-images.githubusercontent.com/59748598/164296322-c0ba92cf-d026-4a1c-95b6-d68022799132.png">


和leetcode 63很像，多了一个上下左右的判断，所以可以看成小岛+dp，上下左右操作的时候，不需要把字符变成特殊的，只需要对比当前的dp[i][j]和新的dp[i][j] (count)，如果大的话就return，表示之前有更少路线的走过来了，不需要了。当然需要多次进入，万一下一次的count是小的呢

然后有一个很骚的操作，这里看似很多行，题目说就三行，所以是第三行next不是
nextLine

```` 
import java.util.*;

public class Main{
    private static int len;
    private static char[][] chars;
    private static int[][] dp;
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        len=scanner.nextInt();
        //int startY=scanner.nextInt(); 
        //int startX=scanner.nextInt();
        //int endY=scanner.nextInt(); 
        //int endX=scanner.nextInt();
        

        int startY = scanner.nextInt(),startX = scanner.nextInt(),endY = scanner.nextInt(),endX = scanner.nextInt();
        
        chars=new char[len][len];
        dp=new int[len][len];
        for(int i=0;i<len;i++){
            chars[i]=scanner.next().toCharArray();
        }
        dfs(startX,startY,1,endX,endY);
        System.out.println(dp[endX][endY]-1);
        
        
    }
    private static void dfs(int x,int y,int count,int endX,int endY){
        if(x<0 || x>=len || y<0 || y>=len){
            return;
        }
        if(chars[x][y]=='#' || chars[x][y]=='@'){
            return;
        }
        
        if(dp[x][y]!=0 && dp[x][y]<=count){
            return;
        }
        dp[x][y]=count;
        if (x == endX && y == endY) return;
        count ++;
        dfs(x - 1,y,count,endX,endY);
        dfs(x + 1,y,count,endX,endY);
        dfs(x,y - 1,count,endX,endY);
        dfs(x,y + 1,count,endX,endY);
    }
    
    
    
    
    
}
````
