这道题严谨来说是找下一个更大，尽可能找下一个就比现在这个稍微大一个就好，原理在最下面那张解释图

这里的找下一个最大，远离很难实现很简单，只要整个数组不是完全从大到小，从后往前找到最后一个降序，在从后找第一个比这个降大的，交换，在sort后面就好了

以求 12385764 的下一个排列为例，找到5（第一个下降的）：
<img width="786" alt="Screen Shot 2022-01-19 at 6 00 50 PM" src="https://user-images.githubusercontent.com/59748598/150249564-b68b31ed-bb2f-4c46-8874-af0afbf8cc76.png">
在找到6（从后面第一个比5大的）
<img width="778" alt="Screen Shot 2022-01-19 at 6 01 59 PM" src="https://user-images.githubusercontent.com/59748598/150250151-c06fd494-e560-4bfd-b2fe-1a8bbfb81e76.png">

交换5 6
![image](https://user-images.githubusercontent.com/59748598/150250274-c7019046-44bf-44ed-a3ea-5eeec2a942c0.png)

因为754是从大到小，可以reverse也可以直接sort
![image](https://user-images.githubusercontent.com/59748598/150250649-9ea0ce3a-480b-4182-9113-e0fd6c02eebb.png)

对比为什么这样是下一个刚到大一点，首先如果换46 ，47 67同理，必须从后面找到开始下降的，这也是为什么题目给了[1,2,3] [1,3,2]，其次，找到左边这个要和右边的某个替换，自然是找从后面右边刚好比他大的，
如果是找到7的话 12386457 > 12387456.  (因为是尽量小，从left+1自然是从小到大,所以可以sort也可以reverse)
![image](https://user-images.githubusercontent.com/59748598/150251492-9990725f-8921-4b7b-a1a3-b34f869076a7.png)

这里有一个小问题，sort的时候 Array.sort(int[], startIndex,endIndex)这个endIndex和substring一样，要+1


```` 
class Solution {
    public void nextPermutation(int[] nums) {
        //corner case
        if(nums.length<=1) return;
        
        //从后往前找到第一个变小的
        int left=-1;
        for(int i=nums.length-2;i>=0;i--){
            if(nums[i]<nums[i+1]){
                left=i;
                break;
            }
            
        }
        if(left==-1){
            //意味着这个nums是从大到小，直接reverse或者sort，return
            Arrays.sort(nums);
            //reverse(nums,0,nums.length-1);
            return;
        }
        //现在意味着找到了firstSmall
        //现在继续从后往前找[firstSmall+1,end]里第一个比firstSmall大的
        int right=-1;
        for(int i=nums.length-1;i>=0;i--){
            if(nums[i]>nums[left]){
                right=i;
                break;
            }
            
        }
        swap(nums,left,right);
        
        //reverse(nums,left+1,nums.length-1);
        
        int len=nums.length;
        //Arrays.sort(nums,left+1,len);
        Arrays.sort(nums,left+1,len);
        
        
    }
    
    private void swap(int[] nums,int i,int j){
        int temp=nums[i];
        nums[i]=nums[j];
        nums[j]=temp;
    }
    
    private void reverse(int[] nums,int i,int j){
        while(i<j){
            swap(nums,i,j);
            i++;
            j--;
        }
        
    }
    
    
    
}
````







