<img width="709" alt="Screen Shot 2022-08-17 at 5 07 55 PM" src="https://user-images.githubusercontent.com/59748598/185264660-cfd01087-84fc-4ada-88eb-86fb21b06b60.png">

就是构图，然后每次选中一个点dfs，找到最大的path

在判断path的时候，出了没有visite过，还要判断点权>0，因为这个edge是根据point[]数组点权相减得来的

```` 
import java.util.*;

//无向图
public class Main{
    public static int max=0;
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int[] points=new int[n+1];
        for(int i=1;i<=n;i++){
            points[i]=sc.nextInt();
        }
        Map<Integer,LinkedList<Integer>> graph=new HashMap<>();
        for(int i=0;i<n-1;i++){
            int point1=sc.nextInt();
            int point2=sc.nextInt();
            if(graph.containsKey(point1) && (point2>=point1)){
                LinkedList<Integer> list=graph.get(point1);
                list.add(point2);
            }
            else{
                LinkedList<Integer> list=new LinkedList<>();
                list.add(point2);
                graph.put(point1,list);
            }
            //point 2
            if(graph.containsKey(point2)&& (point1>=point2)){
                LinkedList<Integer> list=graph.get(point2);
                list.add(point1);
            }
            else{
                LinkedList<Integer> list=new LinkedList<>();
                list.add(point1);
                graph.put(point2,list);
            }
        }
        
        //built graph
        for(int i=1;i<=n;i++){
            dfs(points,graph,1,new HashSet<>(),i);
        }
        System.out.println(max);
        
        
        
    }
    public static void dfs(int[] arr,Map<Integer,LinkedList<Integer>> graph,int weights,
                          HashSet<Integer> visited,int current){
        max=Math.max(weights,max);
        for(int point : graph.get(current)){
            if(!visited.contains(point)&& arr[point]>arr[current]){
                visited.add(point);
                dfs(arr,graph,weights+1,visited,point);
            }
        }
        
        
    }
    
    public static void helper(int n,Map<Integer,LinkedList<Integer>> graph){
        for(int i=1;i<=n;i++){
            System.out.print("point "+i+" -> ");
            for(int num : graph.get(i)){
                System.out.print(" "+num);
            }
            System.out.println();
        }
    }
    
}



````

