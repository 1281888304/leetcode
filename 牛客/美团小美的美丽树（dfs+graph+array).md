<img width="750" alt="Screen Shot 2022-05-16 at 11 30 11 AM" src="https://user-images.githubusercontent.com/59748598/168658865-f1206968-2548-40a7-9bab-f4d75ee02c50.png">

<img width="162" alt="Screen Shot 2022-05-16 at 11 30 20 AM" src="https://user-images.githubusercontent.com/59748598/168658887-96b51c32-022b-4fdb-aff7-1039bf1e57b0.png">

这是一个无根树，就可以看成一个graph，找出子节点<=k (childNum[i]<=k)然后这个子节点最大差（各个节点权重，这里的给的是从1开始到5，题目说了从1到N），用weight数组存起来，最大最小也用max/min数组存起来

关于点权weigit并不是顺序从1到5，这里是第一个点权是1，第二个是3，第三个是2，weight数组的index索引代表index，value代表权重

然后最下面给的root并不是weight这个3，而是weight为2的这个第三个点，用hashmap把点和点连接起来，这里要注意是无向图，所以要把两边都存了

然后就搜索，每次dfs的时候，搜索map得到的child，然后更新最大和最小还有childNum子树数量，然后对比是否需要更新resNode

```` 
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.HashMap;
import java.util.ArrayList;

public class Main {
    static boolean[] visited;   // 标记节点是否已经被访问
    static int[] weight;        // 节点权值,1 2,3 4,5
    static int[] childNum;      // 存储以节点i为根的树有多少个节点
    static int[] max, min;      // 存储以节点i为根的子树下的最大值和最小值
    // 节点间的最大差值
    static int maxDiff = -1;
    // 待求节点
    static int resNode = -1,node=-1;
    // 邻接表
    static HashMap<Integer, ArrayList<Integer>> tree;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] temp = br.readLine().trim().split(" ");
        int n = Integer.parseInt(temp[0]);
        int k = Integer.parseInt(temp[1]);
        temp = br.readLine().trim().split(" ");
        weight = new int[n + 1];
        for(int i = 1; i <= n; i++) weight[i] = Integer.parseInt(temp[i - 1]);
        int x, y;
        // 构建树图的邻接表
        tree = new HashMap<>();
        ArrayList<Integer> list;
        for(int i = 1; i <= n - 1; i++){
            temp = br.readLine().trim().split(" ");
            x = Integer.parseInt(temp[0]);
            y = Integer.parseInt(temp[1]);
            if(tree.containsKey(x)){
                list = tree.get(x);
                list.add(y);
                //tree.put(x, list);
            }else{
                list = new ArrayList<>();
                list.add(y);
                tree.put(x, list);
            }
            if(tree.containsKey(y)){
                list = tree.get(y);
                list.add(x);
                //tree.put(y, list);
            }else{
                list = new ArrayList<>();
                list.add(x);
                tree.put(y, list);
            }
        }
        int root = Integer.parseInt(br.readLine().trim());
        visited = new boolean[n + 1];
        max = new int[n + 1];
        min = new int[n + 1];
        childNum = new int[n + 1];
        dfs2(root, k);
        System.out.println(resNode);
    }
    
    public static void dfs2(int root,int k){
        visited[root]=true;
        max[root]=weight[root];
        min[root]=weight[root];
        
        childNum[root]=1;
        
        for(int child : tree.get(root)){
            if(!visited[child]){
                dfs2(child,k);
                max[root]=Math.max(max[root],max[child]);
                min[root]=Math.min(min[root],min[child]);
                childNum[root]=childNum[root]+childNum[child];
            }
            
        }
        if(childNum[root]<=k && max[root]-min[root]>=maxDiff){
            if(max[root]-min[root]>maxDiff){
                maxDiff=max[root]-min[root];
                resNode=root;
            }
            else{
                resNode=(resNode==-1)? root :Math.min(resNode,root);
            }
        }
        
    }

}
````










