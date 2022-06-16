https://www.nowcoder.com/practice/76039109dd0b47e994c08d8319faa352?tpId=295&tqId=1008104&ru=/exam/oj&qru=/ta/format-top101/question-ranking&sourceUrl=%2Fexam%2Foj

https://www.nowcoder.com/practice/76039109dd0b47e994c08d8319faa352?tpId=295&tqId=1008104&ru=/exam/oj&qru=/ta/format-top101/question-ranking&sourceUrl=%2Fexam%2Foj

<img width="753" alt="Screen Shot 2022-06-15 at 5 54 26 PM" src="https://user-images.githubusercontent.com/59748598/173968005-9601ee5e-2a96-4ca3-b2f6-00ee8fe0b692.png">

这里有一个问题，看起来直接后一个比前一个小直接给1，但是有一个问题就是如果是比如说


 [1,2,3,2,1] 我们的dp是[1,2,3,1,1] 这样最后两个就错了，2比1大
 
 所以左边遍历一遍，右边也要来一遍确保两边都没有问题

变成[1,2,3,2,1]


代码：
```` 
import java.util.*;
public class Solution {
    public int candy (int[] arr) {
        int n=arr.length;
        if(n<=1)
            return n;
        int[] nums = new int[n];
        //初始化
        for(int i = 0; i < n; i++)
            nums[i] = 1;
        //从左到右遍历
        for(int i = 1; i < arr.length; i++){ 
            //如果右边在递增，每次增加一个
            if(arr[i] > arr[i - 1]) 
                nums[i] = nums[i - 1] + 1; 
        }
        //记录总糖果数
        int res = nums[arr.length - 1]; 
        //从右到左遍历
        for(int i = arr.length - 2; i >= 0; i--){ 
             //如果左边更大但是糖果数更小或者一样
            if(arr[i] > arr[i + 1] && nums[i] <= nums[i + 1])
                nums[i] = nums[i + 1] + 1; 
            //累加和
            res += nums[i]; 
        }
        return res;
    }
}

````

