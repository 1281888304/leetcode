<img width="1060" alt="Screen Shot 2022-05-02 at 5 31 59 PM" src="https://user-images.githubusercontent.com/59748598/166349676-17977388-4cf1-4e1f-aba1-34a2c1eca53e.png">

房子只能看到左边/右边单调递减和自己

就是先来一遍从右到左，判断向右看能有多少，利用stack.size来判断，stack是单调递减的stack。

判断完右边有多少个，再来一次单调递减从左到右，看左边有多少个,还是单调递减

然后加起来在+1

```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param heights int整型一维数组 
     * @return int整型一维数组
     */
    public int[] findBuilding (int[] heights) {
        // write code here
        LinkedList<Integer> stack=new LinkedList<>();
        int n=heights.length;
        int[] right=new int[n];
        for(int i=n-1;i>=0;i--){
            right[i]=stack.size();
            while(!stack.isEmpty() && heights[i]>=heights[stack.peek()]){
                stack.pop();
            }
            
            stack.push(i);
        }
        stack.clear();
        int[] left=new int[n];
        for(int i=0;i<n;i++){
            left[i]=stack.size();
            while(!stack.isEmpty() && heights[i]>=heights[stack.peek()]){
                stack.pop();
            }
            stack.push(i);
        }
        
        int[] total=new int[n];
        for(int i=0;i<n;i++){
            total[i]=left[i]+right[i]+1;
        }
        return total;
        
    }
}
````




