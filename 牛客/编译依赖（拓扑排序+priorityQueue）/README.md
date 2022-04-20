https://www.nowcoder.com/test/question/74d0c1b6bb5a403a84093d0ffdc58ee2?pid=29582167&tid=55553837

<img width="1129" alt="Screen Shot 2022-04-19 at 11 26 31 PM" src="https://user-images.githubusercontent.com/59748598/164164143-36d54853-fad5-456b-abce-4aef884655f8.png">

首先第一步肯定是把string数组换成int，用split

![image](https://user-images.githubusercontent.com/59748598/164164313-8e97b2f7-c1ef-4d3e-b085-349f162c0968.png)

然后看看哪个是-1（不需要依赖就放进queue），放的是索引index，索引刚好是依赖的，每次拿出来然后就遍历数组，看看哪个和索引一样，就把他的也offer到queue

这里说明了是生序，所以用priorityQueue，然后记得最后delete掉一个就好了

 
```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     * 编译顺序
     * @param input string字符串 
     * @return string字符串
     */
    public String compileSeq (String input) {
        String[] str=input.split(",");
        int[] arr=new int[str.length];
        for(int i=0;i<str.length;i++){
            arr[i]=Integer.parseInt(str[i]);
        }
        
        PriorityQueue<Integer> queue=new PriorityQueue<>();
        //boolean[] visited=new boolean[arr.length];
        for(int i=0;i<arr.length;i++){
            if(arr[i]==-1){
                queue.offer(i);
            }
        }
        StringBuilder sb=new StringBuilder();
        while(!queue.isEmpty()){
            int temp=queue.poll();
            //visited[temp]=true;
            sb.append(temp).append(",");
            for(int i=0;i<arr.length;i++){
                if(arr[i]==temp ){
                    queue.offer(i);
                }
            }
        }
        sb.deleteCharAt(sb.length()-1);
        return sb.toString();
    }
}
````




