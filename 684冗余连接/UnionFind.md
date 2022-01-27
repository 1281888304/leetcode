<img width="619" alt="Screen Shot 2022-01-26 at 6 04 05 PM" src="https://user-images.githubusercontent.com/59748598/151278686-c8e61970-0146-476e-95a7-41b2cb131052.png">

找到多余的边，返回。简单操作就是unionfind，如果找到父类是一样的，就返回，不是的话就连在一起

```` 
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] res=null;
        //从1开始，0被跳过了+1
        UnionFind uf=new UnionFind(edges.length+1);
        for(int[] edge : edges){
            int source=edge[0];
            int target=edge[1];
            if(uf.find(source)==uf.find(target)){
                return edge;
            }else{
                uf.union(source,target);
            }
        }
        return null;
    }
}


class UnionFind{
    int[] parent;
    
    public UnionFind(int n){
        parent=new int[n];
        for(int i=0;i<n;i++){
            parent[i]=i;
        }
    }
    
    public int find(int x){
        while(x!=parent[x]){
            x=parent[x];
        }
        return x;
    }
    
    public void union(int x,int y){
        parent[find(x)]=y;
    }
}
````




