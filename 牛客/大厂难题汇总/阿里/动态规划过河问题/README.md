



<img width="688" alt="Screen Shot 2022-07-26 at 3 19 16 PM" src="https://user-images.githubusercontent.com/59748598/181122075-98cbf52e-bc9b-4ea3-8128-4ae8768cc090.png">

<img width="287" alt="Screen Shot 2022-07-26 at 3 19 30 PM" src="https://user-images.githubusercontent.com/59748598/181122107-19f5ca3a-df09-4907-b613-46eea1cc8719.png">

经典问题，一去一回，然后当n>=4 四个人以上有两种套路，

1 最轻的一个一去一回带人 （最后最轻的把船开回来）
2 最轻+第二轻（最轻的回来） 然后最重的和倒数第二重过去，第二轻的把船开回来


每次处理两个然后把船开回来，然后三个人两个人一个人（n<=3）就好判断了，都是一种办法

代码：
```` 
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        int T=sc.nextInt();
        for(int k=0;k<T;k++){
            int n=sc.nextInt();
            int[] arr=new int[n];
            for(int i=0;i<n;i++){
                arr[i]=sc.nextInt();
            }
            System.out.println(helper(arr,n));
        }
        
        
        
    }
    
    public static int helper(int[] arr,int n){
        Arrays.sort(arr); 
        int res=0;
        //每次处理最大的两个
        while(n>=4){
            res+=Math.min(arr[0]*2+arr[n-1]+arr[n-2],
                            arr[0]+arr[1]+arr[n-1]+arr[1]);
            n=n-2;
        }
        if(n==3){
            res+=arr[0]+arr[1]+arr[2];
                         
        }
        else if(n==2){
            res+=arr[1];
        }
        else if(n==1){
            res+=arr[0];
        }
        return res;
    }
}

````

