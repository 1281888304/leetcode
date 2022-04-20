```` 
import java.util.*;

public class Main{
    private static int len;
    private static char[][] chars;
    private static int[][] dp;
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        len=scanner.nextInt();
        int startY=scanner.nextInt(); 
        int startX=scanner.nextInt();
        int endY=scanner.nextInt(); 
        int endX=scanner.nextInt();
        chars=new char[len][len];
        dp=new int[len][len];
        for(int i=0;i<len;i++){
            chars[i]=scanner.nextLine().toCharArray();
        }
        dfs(startX,startY,0,endX,endY);
        System.out.println(dp[endX][endY]-1);
        
        
    }
    private static void dfs(int x,int y,int count,int endX,int endY){
        if(x<0 || x>=len || y<0 || y>=len){
            return;
        }
        if(chars[x][y]=='#' || chars[x][y]=='@'){
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
