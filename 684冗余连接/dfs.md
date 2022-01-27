<img width="601" alt="Screen Shot 2022-01-26 at 5 44 04 PM" src="https://user-images.githubusercontent.com/59748598/151276429-e827a869-e809-4cb6-9a32-2c379dabc608.png">

无向图用hashmap创建一张图，然后把每条边加上去[1,2] => Map{1:2 ; 2:1} 然后遍历每一条边，比如说 [1,2] [1,3]理论上就可以从1 2 3随便走，因为不是有向的，这个时候多一个[2,3]就可以删掉了

```` 
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        int[] res=null;
        int len=edges.length; //多少个点就有多少条边
        //graph
        Map<Integer,List<Integer>> graph=new HashMap<>();
        for(int i=1;i<=len;i++){
            graph.put(i,new ArrayList<>());
        }
        //visited
        Set<Integer> visited=new HashSet<>();
        
        for(int[] edge: edges){
            int source=edge[0];
            int target=edge[1];
            visited.clear(); //clean and re-do the search
            //if find without add this edge
            //可以顺过去，返回答案
            if(dfs(source,target,visited,graph)){
                res=edge;
                return res;
            }else{
                //add edge and build graph
                //不能顺过去，构建图
                graph.get(source).add(target);
                graph.get(target).add(source);
            }
        }
        return res;
    }
    
    public boolean dfs(int source,int target,Set<Integer> visited,
                   Map<Integer,List<Integer>> graph){
        if(source==target) return true;
        for(int nei : graph.get(source)){
            if(!visited.contains(nei)){
                visited.add(nei);
                if(nei==target) return true;
                boolean res=dfs(nei,target,visited,graph);
                if(res) return res;
            }
        }
        return false;
    }
}
````




