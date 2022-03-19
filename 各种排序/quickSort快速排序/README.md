https://leetcode.com/submissions/detail/593227771/


https://blog.csdn.net/wthfeng/article/details/78037228

一个arr选定一个基数，一般是第一个，在arr里找这个左比这个基数大和右边基数小的，交换，然后重复不停的递归把交换好的在sort

最后一步是把第一个base基数，挪到j，因为j是最后一个比base大的

几个注意事项：

1 最后一步交换j和一开始的base，不是j-1，因为到了最后出来的时候肯定是i==j这个j后面和i前面都排好了，直接和这个i/j交换

![image](https://user-images.githubusercontent.com/59748598/159137118-4b3fd913-2c5c-445b-8e0a-9dad7d630684.png)
图上带下划线的是交换过的


```` 
//交换最左边的check和j-1(j是比check大中最小的)
        swap(nums,start,i);
        quickSort(nums,start,j-1);
        quickSort(nums,j+1,end);
````

2 利用递归的时候，利用i/j把这个大的array分成几个小的array，记住这个j不需要进入递归，因为左边右边都排好了，单独排左边右边就可以了不然有bug

```` 
//交换最左边的check和j-1(j是比check大中最小的)
        swap(nums,start,i);
        quickSort(nums,start,j-1);
        quickSort(nums,j+1,end);
````


3 用start/end或者low/high划分array，记得要判断start>=end或者low>=high不能光判断==，因为如果递归下来刚好只有两个的时候，下一次递归的start肯定比end大

[1,2]=》递归成[1]这个时候start是1（0+1）,end是0（1-1）


```` 
if(start>=end) //means only one element in temp array
            return;
````

4 存在重复数组的时候，和base判断的时候要用>= / <=
```` 
 while(i<j){
            //找到右边比check小的
            while(nums[j]>=base && i<j){
                j--;
            }
            //找到左边比check大的
            while(nums[i]<=base&& i<j){
                i++;
            }
            
            swap(nums,i,j);
        }
````

完整代码：
```` 
class Solution {
    public int[] sortArray(int[] nums) {
        quickSort(nums,0,nums.length-1);
        return nums;
    }
    
    public void quickSort(int[] nums,int start,int end){
        if(start>=end) //means only one element in temp array
            return;
        int base=nums[start];
        int i=start,j=end;
        while(i<j){
            //找到右边比check小的
            while(nums[j]>=base && i<j){
                j--;
            }
            //找到左边比check大的
            while(nums[i]<=base&& i<j){
                i++;
            }
            
            swap(nums,i,j);
        }
        //交换最左边的check和j-1(j是比check大中最小的)
        swap(nums,start,i);
        quickSort(nums,start,j-1);
        quickSort(nums,j+1,end);
        
    }
    
    
    
    public void swap(int[] nums,int i,int j){
        int temp=nums[i];
        nums[i]=nums[j];
        nums[j]=temp;
    }
}
````

