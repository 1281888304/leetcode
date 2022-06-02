当一定有答案的时候，可以使用二分查找，首先任务就是判断什么情况下left要往右移动即 left=mid+1，这个情况下right =mid,套用while(left<right),

如果是while(left<=right),里面必须返回一个即结果

同样道理如果是先判断往右走，也是r=mid 然后else left=mid+1

对比leetcode 162两种写法
```` 
public int findPeakElement (int[] nums) {
        // write code here
        int left=0,right=nums.length-1;
        
        //一定有答案的话,left<mid核心理念是left和right可以不动，
        //所以这里的else看起来满足答案也不用处理
        while(left<=right){
            int mid=left+(right-left)/2;
            if(nums[mid]<nums[mid+1]){
                left=mid+1;
            }
            else{
                right=mid;
            }
            
        }
        return left;
        
    }
````


```` 
public int findPeakElement(int[] nums) {
        int l = 0, r = nums.length - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (nums[mid] > nums[mid + 1])
                r = mid;
            else
                l = mid + 1;
        }
        return l;
    }
````

普通的基础查找也可以使用二分法，while(left<mid)只不过最后要多加一个判断，判断left/right需不需要返回-1

```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param nums int整型一维数组 
     * @param target int整型 
     * @return int整型
     */
    public int search (int[] nums, int target) {
        // write code here
        if(nums.length<1) return -1;
        int left=0,right=nums.length-1;
//         while(left<=right){
//             int mid=left+(right-left)/2;
//             if(nums[mid]==target){
//                 return mid;
//             }
//             else if(nums[mid]<target){
//                 left=mid+1;
//             }
//             else{
//                 right=mid-1;
//             }
//         }
        while(left<right){
            int mid=left+(right-left)/2;
            if(nums[mid]<target){
                left=mid+1;
            }
            else{
                right=mid;
            }
        }
        if(nums[left]==target){
            return left;
        }
        else{
            return -1;
        }
    }
}
````



