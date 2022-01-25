dfs的本质就是构建一张图，把所有email都连起来，然后通过设置visited来不让图的遍历变成死循环

<img width="855" alt="Screen Shot 2022-01-24 at 10 56 15 PM" src="https://user-images.githubusercontent.com/59748598/150926611-e807c698-69fa-4da8-93d3-a50ecd0cc0b4.png">

```` 
//graph: https://www.youtube.com/watch?v=5v6vqoJlfE4
//union: https://leetcode.com/problems/accounts-merge/discuss/109157/JavaC%2B%2B-Union-Find
class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        List<List<String>> res=new ArrayList<>();
        
        if(accounts==null || accounts.size()==0) return res;
        
        //把每个email和username一一对应
        Map<String,String> emailToName=new HashMap<>();
        //把每个email和它的邻居连通的email连接在一起,set是为了不重复
        Map<String,Set<String>> graph=new HashMap<>();
        //放入所有email
        Set<String> emails=new HashSet<>();
        //用于dfs是否访问过
        Set<String> visited=new HashSet<>();
        
        //遍历
        for(List<String> list : accounts){
            String name=list.get(0); //取出名字
            for(int i=1;i<list.size();i++){
                String email=list.get(i);
                emailToName.put(email,name);
                emails.add(email);
                //如果是空的(之前没这个email作为key)就放入一个email
                //这个图保证了每一个email都有专属的图
                graph.putIfAbsent(email,new HashSet<String>());
                if(i==1) continue; //取到了一个邮箱地址，没办法连接其他的邮箱
                //如果是第二个email，就连接当前email Node和之前的email Node
                graph.get(list.get(i-1)).add(email);
                graph.get(email).add(list.get(i-1));
            }
        }
        //遍历无向图
        for(String e : emails){
            if(!visited.contains(e)){
                visited.add(e);
                List<String> tmp=new ArrayList<>();
                tmp.add(e);
                //拿到所有邻居emails，一层层往下遍历,得到所有的emails存在tmp
                dfs(e,graph,visited,tmp);
                Collections.sort(tmp);
                //加上名字
                tmp.add(0,emailToName.get(e));
                res.add(tmp);
            }
            
        }
        return res;
        
    }
    //去到所有邻居emails
    private void dfs(String e,Map<String,Set<String>> graph,Set<String> visited,
                    List<String> tmp){
        //如果遍历过就不管了，下一个，所以这里两个相同的nei用visited来做运动（往下一个走）遍历
        for(String nei : graph.get(e)){
            if(!visited.contains(nei)){
                visited.add(nei);
                tmp.add(nei);
                dfs(nei,graph,visited,tmp);
            }
        }
    }
}
````




