<img width="577" alt="Screen Shot 2022-01-26 at 6 53 23 PM" src="https://user-images.githubusercontent.com/59748598/151283621-8458d860-ce73-4201-ba4a-ca69928562ab.png">

题目给了一个相似的例子，然后一个个对比就好，重点就是构建链接，既然是String的，就用hashmap构建UnionFInd的连接，在find的时候，第一次肯定找不到，然后给自己put一个parent


和947删除多余的石头类似，947多了一个size

然后union的时候，就是Integer。parent[find(x)]=find(y)的变形     parent.put(find(x),find(y));

```` 
class Solution {
    public boolean areSentencesSimilarTwo(String[] sentence1, String[] sentence2, List<List<String>> similarPairs) {
        if(sentence1.length!=sentence2.length) return false;
        UnionFind uf=new UnionFind();
        for(List<String> pair : similarPairs){
            
            String word1=pair.get(0);
            String word2=pair.get(1);
            //连接word1 word2
            uf.union(word1,word2);
        }
        
        //connected
        for(int i=0;i<sentence1.length;i++){
            String word1=sentence1[i];
            String word2=sentence2[i];
            if(!uf.find(word1).equals(uf.find(word2))){
                return false;
            }
        }
        return true;
        
    }
}


class UnionFind{
    //key : cur  |. value : parent
    Map<String,String> parent;
    
    public UnionFind(){
        parent=new HashMap<>();
    }
    
    public String find(String x){
        //第一次放入的时候找不到，设定为自己是自己的parent
        if(!parent.containsKey(x)){
            parent.put(x,x);
        }
        
        //contains
        while(x!=parent.get(x)){
            x=parent.get(x);
        }
        
        return x;
    }
    
    //设置x的parent是y，不可以直接一行，因为设置自己parent在find进行
    //要通过find设置parent
    public void union(String x,String y){
        // String rootX=find(x);
        // String rootY=find(y);
        // if(rootX.equals(rootY)){
        //     return;
        // }
        // parent.put(rootX,rootY);
        parent.put(find(x),find(y));
    }
}
````






