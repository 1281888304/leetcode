这里用指针实现prefix sum， 如果sum大于target，就在里面while loop循环，把最左边删掉，左指针往右走一步

最后判断一下是否为成功


```` 
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left=0;
        int sum=0;
        int min=Integer.MAX_VALUE;
        for(int i=0;i<nums.length;i++){
            sum+=nums[i];
            while(sum>=target){
                min=Math.min(i-left+1,min);
                //把最左边删掉，左指针往右走一步
                sum-=nums[left];
                left+=1;
            }
        }
        return min==Integer.MAX_VALUE? 0 : min;
    }
}
````


