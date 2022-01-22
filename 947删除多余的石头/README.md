
<img width="690" alt="Screen Shot 2022-01-22 at 12 11 56 AM" src="https://user-images.githubusercontent.com/59748598/150630517-bca4b5ed-9d2a-42d0-9f2e-d3d1cfd20223.png">

找到有多少个可以连在一起的，用总长度-连通集合数得到答案

可以选择用map（key current节点，value 父亲节点）或者array，leetcode 947这种判断一共有多少个连通集合，用map更好，因为每次查找可以通过contains判断是否有，每次出现一次+1， 而且map是每一次连接的时候判断是否出现过（containsKey），map的size才会+1，array是一开始就设定好root的父节点是自己，只能通过判断父亲节点是否为自己来判断是否出现过， 但是如果这个root刚好是之前出现过但是也是其中一个连通集合的root（即父亲节点还是本身），就没办法判断出现了几次。还要通过添加visited HashSet判断，很浪费速度。



```` 
class Solution {
    public int removeStones(int[][] stones) {
        UnionFind2 uf=new UnionFind2(stones.length+20000);
        //UnionFind uf=new UnionFind();
        for(int[] stone : stones){
            uf.union(stone[0] + 10001, stone[1]);
            //System.out.print(" "+uf.getSize());
        }
        //去除多少个就变成原来总长度-连通合集总数
        return stones.length - uf.getSize();
        
//         UnionFind uf=new UnionFind();
        
//         for(int[] stone : stones){
//             uf.union(stone[0] + 10001, stone[1]);
//         }
//         //去除多少个就变成原来总长度-连通合集总数
//         return stones.length - uf.getSize();
    }
}

 class UnionFind{
    //无向图 key: current value: parent
    private Map<Integer,Integer> parent;
    //有多少个合集，连在一起的算一个
    private int size;
    
    //初始化构造器
    public UnionFind(){
        this.parent=new HashMap<>();
        this.size=0;
    }
    
    //返回有多少个合集
    public int getSize(){
        return this.size;
    }
    
    //如果有连接的话，找到他的root节点
    public int find(int x){
        //如果没有的话父节点设为自己，连通合集总数+1
        if(!parent.containsKey(x)){
            parent.put(x,x);
            this.size++;
        }
        
        //如果有的话,就是说父节点不是自己
//         if(x!=parent.get(x)){
//             //通过层层递归，找到root，并且替换回来
//             parent.put(x,find(parent.get(x)));
//         }
        
//         return parent.get(x);
        
        //第二种写法，不用递归，用while
        while(parent.get(x) !=x){
            x=parent.get(x);
        }
        return x;
        
        
    }
    
    //连接 x,y 如果他们的root是同一个就算了，不然就连接在一起
    public void union(int x,int y){
        int rootX=find(x);
        int rootY=find(y);
        if(rootX==rootY){
            return;
        }
        
        //连接两个根结点，这样就可以吧rootX和rootY所有children节点都连在一起
        parent.put(rootX,rootY);
        this.size--;
    }
   
}

class UnionFind2{
    int[] parent;
    int size;
    Set<Integer> visited;
    
    public UnionFind2(int n){
        this.size=0;
        parent=new int[n];
        for(int i=0;i<parent.length;i++){
            parent[i]=i;
        }
        visited=new HashSet<>();
    }
    
    public int getSize(){
        return this.size;
    }
    
    public int find(int x){
        if(x==parent[x] && !visited.contains(x)){
            this.size++;
            visited.add(x);
        }
        while(x!=parent[x]){
            x=parent[x];
        }
        
        return x;
        // if(parent[x]!=x){
        //         parent[x] = find(parent[x]);
        //     }
        //     return parent[x];
    }
    //也可以改成boolean判断是否连接成功还是本来就是连接的
    public void union(int x,int y){
        int rootX=find(x);
        int rootY=find(y);
        if(rootX==rootY){
            return;
        }
        
        parent[rootX]=rootY;
        
        this.size--;
    }
    
    
}


class UnionFind3{
    int[] parent;
    int size;
    
    public UnionFind3(int n){
        this.size=n;
        parent=new int[n];
        for(int i=0;i<parent.length;i++){
            parent[i]=i;
        }
    }
    
    public int getSize(){
        return this.size;
    }
    
    public int find(int x){
        while(x!=parent[x]){
            x=parent[x];
        }
        
        return x;
        // if(parent[x]!=x){
        //         parent[x] = find(parent[x]);
        //     }
        //     return parent[x];
    }
    //也可以改成boolean判断是否连接成功还是本来就是连接的
    public void union(int x,int y){
        int rootX=find(x);
        int rootY=find(y);
        if(rootX==rootY){
            return;
        }
        
        parent[rootX]=rootY;
        
        this.size--;
    }

}


//为什么要+100001，因为要把横坐标和纵坐标都连在一起，把横纵坐标连在一起又区分不了这个1是来自横坐标还是纵坐标，就不确定是否连接，size不好判断了，比如说[1,1] 索性把横坐标加上100001，大出取值范围，然后让100002的父节点是1，这样横纵坐标就连在一起了
````
