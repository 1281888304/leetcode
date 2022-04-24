<img width="1179" alt="Screen Shot 2022-04-23 at 10 32 50 PM" src="https://user-images.githubusercontent.com/59748598/164958088-e6281a5d-f6c3-4b23-805f-d1b98cca9e03.png">

这道题就是从input拿到所有人的score，然后sort，用遍历或者二分查找查到某一个分数可以让所有的人处于这个分数上下就行，需要提前判断是否有答案就好做了

判断完以后，用for loop遍历或者二分判断，每次判断有多少人pass多少人lose，在进行.left<right这种二分一般看left，

这里left和right是人数从1开始，array从0开始return left-1，最后的left代表了从1开始第left个分数合适


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
            //分数低了
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


