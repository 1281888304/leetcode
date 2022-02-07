就很简单了，注意一撸到底的，不需要for loop


```` 
class Solution {
    int res=0;
    public int findTargetSumWays(int[] nums, int target) {
        bt(nums,target,0,0);
        return res;
        
    }
    //一撸到底不需要for
    public void bt(int[] nums,int target,int sum,int index){
        
        if(sum==target && index==nums.length){
            res++;
            return;
        }
        if(index==nums.length) return;
        else{
            sum=sum+nums[index];
            bt(nums,target,sum,index+1);
            sum=sum-nums[index]-nums[index];
            bt(nums,target,sum,index+1);
        }
        
        
    }
}
````

