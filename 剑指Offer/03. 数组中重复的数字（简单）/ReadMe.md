https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/solution/mian-shi-ti-03-shu-zu-zhong-zhong-fu-de-shu-zi-yua/

利用set中add方法，如果重复返回false来判断是否出现过

```` 
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set=new HashSet<>();
        for(int num : nums){
            if(!set.add(num)){
                return num;
            }
        }

        return -1;
    }
}
````

但是set肯定不是最快的，最快的我们可以利用排序的思路去做，我们用一个while loop，不停的把位子在i的数字（nums[i]）放到i==nums[i]这里去，然后玩意放不了了，这就是重复的数字，因为比如说我们有两个2，肯定不能在i=2放两个2，只能放一个2.   然后这里交换的时候记得nums[i] 改变以后要用nums[temp]=temp

![image](https://user-images.githubusercontent.com/59748598/154169215-ead45e82-b302-4832-ab5d-8cd9c6633f81.png)

这里的思路是只有当前我们的i==nums[i]. 当前索引i正确了，我们才能继续往下走，不能的话，一直把当前i放到对的位子

比如说一开始2放到index=2去，这就把1掉过来了

第二步 把1放到index=1，这就把3掉过来了

第三步吧3放到index=3 然后0 3都正确了

然后下面几步一直continue，直到最后一个2，发现之前index=2上面已经有一个2了，直接return

```` 
class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while(i<nums.length){
            //已经交换过或者本来就是按顺序排放的
            if(i==nums[i]){
                i++;
                continue;
            }
            //发现不能交换了，应该排序好的位子，已经有了
            if(nums[i]==nums[nums[i]]){
                return nums[i];
            }

            //交换，把当前nums[i]放到i=nums[i]上
            int temp=nums[i];
            nums[i]=nums[nums[i]];
            nums[temp]=temp;

        }
        return -1;
    }
}
````



