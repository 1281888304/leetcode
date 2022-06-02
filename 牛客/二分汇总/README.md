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




