base和延伸版本

198 213

设置一个dp[n+1]. 为什么是n+1，因为我们从0开始，第0间房假设偷0元
dp[0]=0; //

dp[1]=nums[1] 第一个默认为打劫第一家因为前一家得到0

升级版本213连城环第一家拿了就不能最后一家，最后一家拿了不能第一家，就是简单的把题目拆成两个198，一个是从[0,n-1]. 另外一个[1,n]

```` 
class Solution {
    public int rob(int[] nums) {
        int length = nums.length;
        if (length == 1) {
            return nums[0];
        } else if (length == 2) {
            return Math.max(nums[0], nums[1]);
        }
        return Math.max(robRange(nums, 0, length - 2), robRange(nums, 1, length - 1));
    }

    public int robRange(int[] nums, int start, int end) {
        int first = nums[start], second = Math.max(nums[start], nums[start + 1]);
        for (int i = start + 2; i <= end; i++) {
            int temp = second;
            second = Math.max(first + nums[i], second);
            first = temp;
        }
        return second;
    }
}

//就是简单的分成了两个，第一个array没有第一个，第二个没有最后一个
````

