<img width="552" alt="Screen Shot 2022-02-13 at 12 24 57 PM" src="https://user-images.githubusercontent.com/59748598/153773464-d66dfd55-bda4-4afd-9260-f422419f1b72.png">

这道题目关键就是找到一个最远距离，然后fastest是等于当前距离+可以行走的距离 index+num

![image](https://user-images.githubusercontent.com/59748598/153773497-e222efea-6285-422e-97ac-906b5a0f1603.png)

然后注意如果发现不能继续往下走，不要直接返回false，break然后判断是否到最后一个了

又或者发现如果此时可以走的距离是0，但是最远faestest在后面，直接continue就好

```` 
class Solution {
    public boolean canJump(int[] nums) {
        int n=nums.length;
        if(n<=1) return true;
        
        int fastest=-1;
        
        for(int i=0;i<n;i++){
            int num=nums[i];
            if(num==0){
                if(fastest<=i)
                    break;
                else
                    continue;
            }
            fastest=Math.max(i+num,fastest);
        }
        return fastest>=n-1;
    }
}
````



