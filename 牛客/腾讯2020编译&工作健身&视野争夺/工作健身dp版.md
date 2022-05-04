<img width="1039" alt="Screen Shot 2022-05-03 at 4 57 25 PM" src="https://user-images.githubusercontent.com/59748598/166604566-713d8de8-c9ad-4477-8f7d-dcb66707c654.png">

dp版本把问题看成了，怎么样不工作的时间最多，然后用dp[i][3]存着不同的情况

dp[i][0]/ dp[i][1] /dp[i][2] 表示i天，休息/工作/健身的不休息最大天数，每天看健身房/公司开门情况，然后根据前一天情况判断最大不工作天数。

健身房开门就根据前一天休息/工作，公司开门就根据前一天休息/健身， 休息的话就看前一天的三个数哪个最大，反正休息三个数都不会变

这里因为要判断前一天，用dp[i+1][]来判断实际上第i天，每天的实际结果放在i+1天

```` 
 import java.util.*;

public class Main{
    //0 relax 1 work 2 gym 3 2option
    public static int state=3;
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        int n=Integer.parseInt(scanner.nextLine());
        int[] company=new int[n];
        int[] gym=new int[n];
        String[] input1=scanner.nextLine().split(" ");
        String[] input2=scanner.nextLine().split(" ");
        for(int i=0;i<n;i++){
            company[i]=Integer.parseInt(input1[i]);
            gym[i]=Integer.parseInt(input2[i]);
        }
        int[][] dp=new int[n+1][3];
        //dp[i][0] means relax, dp[i][1] means work dp[i][2]means gym
        for(int i=0;i<n;i++){
            //公司开着，选择去工作，看看是休息/运动哪个不休息的天数多
            if(company[i]==1){
                dp[i+1][1]=Math.max(dp[i][0],dp[i][2])+1;
            }
            //健身房开着，去运动
            if(gym[i]==1){
                dp[i+1][2]=Math.max(dp[i][0],dp[i][1])+1;
            }
            //休息，不休息的天数不需要➕1
            dp[i+1][0]=Math.max(dp[i][0],Math.max(dp[i][1],dp[i][2]));
        }
        int maxNotRelaxDay=Math.max(dp[n][0],Math.max(dp[n][1],dp[n][2]));
        System.out.print(n-maxNotRelaxDay);
        
    }
}
````





