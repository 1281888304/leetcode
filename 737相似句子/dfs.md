<img width="610" alt="Screen Shot 2022-01-26 at 6 22 53 PM" src="https://user-images.githubusercontent.com/59748598/151280502-c424849c-07e0-497f-8d8c-6eda6b28071e.png">

用hashmap创建一张图，然后遍历，不能从source word1找到target word2，返回false

```` 
class Solution {
    public boolean areSentencesSimilarTwo(String[] sentence1, String[] sentence2, List<List<String>> similarPairs) {
        if(sentence1.length!=sentence2.length) return false;
        //build graph
        Map<String,List<String>> graph=new HashMap<>();
        for(List<String> pairList : similarPairs){
            String pair1=pairList.get(0);
            String pair2=pairList.get(1);
            graph.putIfAbsent(pair1,new ArrayList<>());
            graph.putIfAbsent(pair2,new ArrayList<>());
            //connect the graph
            graph.get(pair1).add(pair2);
            graph.get(pair2).add(pair1);
        }
        //done the build graph
        //loop the sentence1 , to check if sentence 2 word is similiar
        Set<String> visited=new HashSet<>();
        for(int i=0;i<sentence1.length;i++){
            String word1=sentence1[i];
            String word2=sentence2[i];
            if(word1.equals(word2))
                continue;
            visited.clear();
            //if dfs find there are not match,return false and that's the result
            if(!dfs(word1,word2,visited,graph)){
                return false;
            }
        }
        
        return true;
    }
    //check if we can found it
    private boolean dfs(String word1, String word2, Set<String> visited,
                       Map<String,List<String>> graph){
        if(word1.equals(word2)) return true;
        if(!graph.containsKey(word1)) return false;
        for(String child : graph.get(word1)){
            
            if(!visited.contains(child) && graph.containsKey(child)){
                visited.add(child);
                if(child.equals(word2)) return true;
                boolean res=dfs(child,word2,visited,graph);
                if(res) return true;
            }
        }
        return false;
        
    }
}
````



