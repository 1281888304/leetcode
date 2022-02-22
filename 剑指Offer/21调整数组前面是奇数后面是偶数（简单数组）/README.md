https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/

<img width="526" alt="Screen Shot 2022-02-22 at 8 33 14 AM" src="https://user-images.githubusercontent.com/59748598/155176397-fc8fb65d-d4df-4a78-9bbb-017e61f63476.png">



没什么好说的写也就花了五分钟，用两个index，一个从后面开始，一个从前面开始放数字

```` 
class Solution {
    public int[] exchange(int[] nums) {
        int n=nums.length;
        int[] res=new int[n];
        int index1=0,index2=n-1;

        for(int i=0;i<n;i++){
            int num=nums[i];
            if(num%2!=0){
                res[index1++]=num;
            }
            else{
                res[index2--]=num;
            }
        }
        return res;
    }
}
````




