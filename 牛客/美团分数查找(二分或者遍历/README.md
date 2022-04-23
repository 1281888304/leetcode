```` 
import java.util.*;

public class Main{
    private static int n,x,y;
     public static void main(String[] args){
         Scanner scanner=new Scanner(System.in);
         String[] input1=scanner.nextLine().split(" ");
         String[] input2=scanner.nextLine().split(" ");
         n=Integer.parseInt(input1[0]);
         x=Integer.parseInt(input1[1]);
         y=Integer.parseInt(input1[2]);
         int[] score=new int[n];
         for(int i=0;i<n;i++){
             score[i]=Integer.parseInt(input2[i]);
         }
         int res=helper(score);
         System.out.println(res);
         
         
     }
    
    public static int helper(int[] score){
        Arrays.sort(score);
        //代表最小的区间*2超过了最大，最大的区间*2小了
        if(x*2>n || y*2<n){
            return -1;
        }
        for(int i=0;i<score.length;i++){
            int lose=i+1;
            int pass=n-lose;
            if(lose>=x && lose<=y && pass>=x && pass<=y){
                return score[i];
            }
        }
        
        //现在一定有答案,mid代表分数是score[mid]
        int left=x,right=y;
        while(left<right){
            int mid=left+(right-left)/2;
            int lose=mid+1;
            int pass=n-mid;
            if(lose<x || pass>y){
                left=mid+1;
            }
            else{
                right=mid;
            }
            
        }
        return score[left-1];
    }
    
    
    
    
    
    
    
    
}
````


