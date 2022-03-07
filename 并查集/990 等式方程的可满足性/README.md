https://leetcode-cn.com/problems/satisfiability-of-equality-equations/

就是基础的union find

主方法里先用一个for loop先连接，连接完如果住方法想要打破的话，（打破不一定返回false，连接过了再打破才返回false）

主要就是找有没有可能连接过的

```` 
class Solution {
    public boolean equationsPossible(String[] equations) {
        UnionFind uf=new UnionFind();
        //先连接所有
        for(String s : equations){
            if(s.charAt(1)=='!') continue;
            char c1=s.charAt(0);
            char c2=s.charAt(3);
            uf.Union(c1,c2);
        }
        //看看会不会打破已经连接过的
        for(String s : equations){
            if(s.charAt(1)=='=') continue;
            char c1=s.charAt(0);
            char c2=s.charAt(3);
            if(uf.find(c1)==uf.find(c2)) return false;
        }
        return true;


    }
}


class UnionFind{
    Map<Character,Character> parent;

    public UnionFind(){
        parent=new HashMap<>();
    }

    public Character find(Character c){
        if(!parent.containsKey(c)){
            parent.put(c,c);
        }
        //find root
        while(c!=parent.get(c)){
            c=parent.get(c);
        }
        return c;
    }

    public void Union(Character c1,Character c2){
        parent.put(find(c1),find(c2));
    }
    
}
````








