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
