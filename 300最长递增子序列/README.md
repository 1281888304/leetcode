<img width="662" alt="Screen Shot 2022-05-18 at 6 04 32 PM" src="https://user-images.githubusercontent.com/59748598/169180399-b9267951-cba1-4e32-b0cd-0a115d4b9670.png">


https://leetcode.cn/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-dong-tai-gui-hua-2/

这个答案用了tails，dp+二分，用tails的方式控制了最大的子序列,每一次遍历都会插入一个数进去，要么是替换，要么是直接插入到后一位，用二分法实现

<img width="682" alt="Screen Shot 2022-05-18 at 6 19 00 PM" src="https://user-images.githubusercontent.com/59748598/169181713-9c6cf80f-76ce-4f6c-a4b9-9e2188062916.png">


<img width="693" alt="Screen Shot 2022-05-18 at 6 07 08 PM" src="https://user-images.githubusercontent.com/59748598/169180615-451f2901-e809-40f1-9295-77e9050dc157.png">

<img width="734" alt="Screen Shot 2022-05-18 at 6 07 25 PM" src="https://user-images.githubusercontent.com/59748598/169180643-4a629dba-a656-45fd-bf1d-ab638448037a.png">

精髓就在于用二分查找 binary search找到一个刚好适合的，就是nums[i]刚好在的位置，并且把他添加上去或者替换

这里的二分法就用的很巧，在这种i<j的时候,并且是先判断是不是小于，没有==break，出来的i可能是1种情况，i==j,到最后如果i/j==res，意味着插入了一个，res++ （这里因为index从0开始，所以要res++）
                                 
我们可以看成比如说一开始res=0，找到index（i/j）的时候，这是res=1，然后如果刚好1是第二个位置（遍历第二个），res=2 （i<j）这个j初始就是新的一个0                              

```` 
// Dynamic programming.
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums.length == 0) return 0;
        int[] tails=new int[nums.length];

        int res=0;
        for(int num : nums){
            int i=0;
            int j=res;
            while(i<j){
                int mid=i+(j-i)/2;
                if(tails[mid]<num) i=mid+1;
                else j=mid;
            }
            tails[j]=num;
            if(j==res) res++;
        }
        return res;
    }
}


````
