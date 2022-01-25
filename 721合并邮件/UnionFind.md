<img width="785" alt="Screen Shot 2022-01-24 at 10 49 11 PM" src="https://user-images.githubusercontent.com/59748598/150925789-40678deb-ed9c-4969-895a-5236f06726ac.png">

合并账户的题解和dfs类似，都是UnionFind，构建联系的图

<img width="598" alt="Screen Shot 2022-01-24 at 10 50 18 PM" src="https://user-images.githubusercontent.com/59748598/150925912-5f09046e-4e31-4c65-acd4-959dbb737779.png">

这里的方法是原来有多少个accounts就有多少个id，比如说第一第二个账户是应该合并的，第一个账户的email id是0（从0开始），第二个账户有个email是johnsmith@mail.com在之前第一个出现过了，id仍然是1，
另外一个john00@mail.com的id是1，但是通过并查集，我么设立id 0是1的父类或者1是0的parent，在下面id to email的时候，添加的id就不是之前设定的，是父类，这样这三个email就同一个id

然后找名字，这里的好处就是不会乱，不管是0还是1，得到的名字都是John

```` 
//这个class 比dfs好就是不乱，
class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        //每个email对应的账户
        Map<String,Integer> emailToId=new HashMap<>();
        int n=accounts.size();
        //一开始没有用union连接起来的账户数量
        UnionFind uf=new UnionFind(n);
        for(int i=0;i<n;i++){
            int num=accounts.get(i).size();
            for(int j=1;j<num;j++){
                String curEmail=accounts.get(i).get(j);
                //如果出现过，就用union merge在一起，因为属于上一个主人
                //没出现过，就给id给他，就是i，即使下一个人一样，也会merge到现在这个id
                if(emailToId.containsKey(curEmail)){
                    
                    //uf.union(i,emailToId.get(curEmail));
                    uf.union(emailToId.get(curEmail),i);
                }
                else{
                    emailToId.put(curEmail,i);
                }
            }
        }
        //现在全部都merge好了，用id to email去重
        Map<Integer,List<String>> idToEmail=new HashMap<>();
        for(Map.Entry<String,Integer> entry : emailToId.entrySet()){
            
            int id=uf.find(entry.getValue());
            
            //找到原来的并且加上现在的
            List<String> emails = idToEmail.getOrDefault(id, new ArrayList<>());
            emails.add(entry.getKey());
            //put自动覆盖
            idToEmail.put(id,emails);
        }
        
        //id配齐了，现在把名字加上
        List<List<String>> res = new ArrayList<>();
        for(Map.Entry<Integer, List<String>> entry : idToEmail.entrySet()){
            List<String> emails = entry.getValue();
            Collections.sort(emails);
            List<String> tmp = new ArrayList<>();
            tmp.add(accounts.get(entry.getKey()).get(0));//先添加用户名
            tmp.addAll(emails);
            res.add(tmp);
        }
        return res;
        
    }
}


class UnionFind{
    int[] parent;
    
    //初始化，设定每个父类暂时是自己
    public UnionFind(int n){
        parent=new int[n];
        for(int i=0;i<n;i++){
            parent[i]=i;
        }
    }
    
    public int find(int x){
        while(parent[x]!=x){
            x=parent[x];
        }
        return x;
    }
    
    public void union(int x,int y){
//         int rootX=find(x);
//         int rootY=find(y);
//         if(rootX==rootY){
//             return;
//         }
        
//         parent[rootX]=rootY;
        //一行的版本
        parent[find(x)]=find(y);
    }
    
}
````



