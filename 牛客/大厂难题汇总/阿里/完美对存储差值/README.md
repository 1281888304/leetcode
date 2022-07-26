<img width="542" alt="Screen Shot 2022-07-26 at 1 21 50 PM" src="https://user-images.githubusercontent.com/59748598/181104845-5d533b9b-9497-4acc-a46b-262ce541cfda.png">

<img width="759" alt="Screen Shot 2022-07-26 at 1 22 14 PM" src="https://user-images.githubusercontent.com/59748598/181104909-18573049-6d7d-48eb-be6a-198a19ecaedc.png">

input是一个二维数组，然后判断ai1+aj1=ai2=aj2.....


比如这里的第一行和第三行是完美对，2 + 20 ==11 + 11== 21 +1

我们把和转换成差，第三行[20,11,1]转成 [-9,-10] 查看之前有没有存储是[-9,-10]的 (第一个差是[2,11,21] -> [9.10]存[-9,-10])

然后第三行存相反数[9,10]

这样我们可以通过get HashMap的key来实现比如说第三行存[9,10] value是1，下一次找到另外一个[9,10]直接和1相加，在下一次+2，类似于前缀和

code:
```` 
import java.util.*;


public class Main{
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        String[] line=sc.nextLine().split(" ");
        int n=Integer.parseInt(line[0]);
        int k=Integer.parseInt(line[1]);
        int[][] arr=new int[n][k];
        for(int i=0;i<n;i++){
            line=sc.nextLine().split(" ");
            for(int j=0;j<k;j++){
                arr[i][j]=Integer.parseInt(line[j]);
            }
        }
        System.out.println(solution(arr,n,k));
    }
    
    public static int solution(int[][] arr,int n,int k){
        int res=0;
        HashMap<ArrayList<Integer>,Integer> map=new HashMap<>();
        for(int i=0;i<n;i++){
            ArrayList<Integer> list1=new ArrayList<>();
            ArrayList<Integer> list2=new ArrayList<>();
            for(int j=1;j<k;j++){
                int temp=arr[i][j]-arr[i][j-1];
                list1.add(temp);
                list2.add(-temp);
            }
            res=res+map.getOrDefault(list1,0);
            map.put(list2,map.getOrDefault(list2,0)+1);
        }
        return res;
    }
}

````


