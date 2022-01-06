这题是621升级版，我们也用一行行的方法去做，但是不冷却了，如果遇到冷却直接结束


<img src="../images/621.png" >

class Solution {

    public String rearrangeString(String s, int k) {
        //corner case
        if(k<=1) return s; 
        HashMap<Character,Integer> map=new HashMap<>();
        PriorityQueue<Map.Entry<Character,Integer>> maxHeap=new PriorityQueue<>((a,b)->{
            return b.getValue()-a.getValue();
        });
        for(char c : s.toCharArray()){
            map.put(c,map.getOrDefault(c,0)+1);
        }
        maxHeap.addAll(map.entrySet());
        StringBuilder sb=new StringBuilder();
        //存储丢掉的
        Queue<Map.Entry<Character,Integer>> queue=new LinkedList<>();
        while(!maxHeap.isEmpty()){
            //把最大的拿出来
            Map.Entry<Character,Integer> cur=maxHeap.poll();
            sb.append(cur.getKey());
            cur.setValue(cur.getValue()-1);
            //这里是精妙的地方，先放先取，这样保证了
            //下一行的第一个不会是上一行的最后一个
            //例子 aabbcc
            
            queue.offer(cur);
            if(queue.size()==k){
                Map.Entry<Character,Integer> entry=queue.poll();
                if(entry.getValue()>0){
                    maxHeap.add(entry);
                }
            }
        }
        //如果有一行填不满，就直接返回了，因为当时Heap是空的
        return sb.length() <s.length() ? "" : sb.toString();
        
        
    }
}

