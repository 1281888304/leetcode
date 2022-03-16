https://leetcode-cn.com/problems/bP4bmD/

![Screen Shot 2022-03-16 at 2 32 34 PM](https://user-images.githubusercontent.com/59748598/158694650-a5730da8-ca64-4065-865f-a337d30219b2.png)

![Screen Shot 2022-03-16 at 2 32 43 PM](https://user-images.githubusercontent.com/59748598/158694672-4c7fab8d-a95d-42ca-af00-37cfc25ac1aa.png)

graph[0]就代表0能去的地方，这道题可以用bfs也可以用dfs

dfs就比较简单了，用current/index确定当前是那个数字，从graph得到接下来能走的数字，不停的往下递归，知道最后一位是target就行。 

target在这里是最后一位数字，graph.length-1

当然这道题主要是下边的bfs，bfs里的queue放的不是int/node节点，而是一个list

代码：
```` 
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        int n=graph.length;
        int target=n-1;

        List<List<Integer>> res=new ArrayList<>();
        List<Integer> list=new ArrayList<>();
        list.add(0);
        dfs(graph,res,target,list,0);
        return res;

    }

    public void dfs(int[][] graph,List<List<Integer>> res,int target,List<Integer> list,
            int current){
        if(list.get(list.size()-1)==target){
            res.add(new ArrayList<>(list));
            return;
        }
        int[] paths=graph[current];
        for(int path:paths){
            list.add(path);
            dfs(graph,res,target,list,path);
            list.remove(list.size()-1);
        }
    }
}
````

BFS：一开始想了很久，怎么样在queue里放int的时候复制list，后来看了答案发现可以直接在queue里放一个List,是真没想到

```` 
LinkedList<Integer> queue=new LinkedList<>();
````
每次pop出来，先拿到List最后一个lastNode判断是不是答案，不是的话就用for loop复制这个list（list复制list还是简单的），然后添加下一个

![image](https://user-images.githubusercontent.com/59748598/158695476-a8d54549-624c-4f9b-8958-80778f922374.png)

完整代码：
```` 
//关键在于queue里存的是List<Integer> 
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        int target=graph.length-1;
        
        List<List<Integer>> res=new ArrayList<>();
        LinkedList<List<Integer>> queue=new LinkedList<>();
        
        List<Integer> start=new ArrayList<>();
        start.add(0);
        queue.offer(start);
        while(!queue.isEmpty()){
            List<Integer> list=queue.pop();
            int lastNode=list.get(list.size()-1);
            if(lastNode==target){
                res.add(new ArrayList<>(list));
                //continue;
            }
            //从graph拿接下来可以走的
            for(int next:graph[lastNode]){
                List<Integer> temp=new ArrayList<>(list);
                temp.add(next);
                queue.offer(temp);
            }
        }
        return res;
    }
}
````






