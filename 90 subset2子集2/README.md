
78的变形，多了要考虑一个重复

这里的i>index保证了如果i=index，然后两个一样是可以加的（回溯的时候可以加），但是从for loop顺上去不可以加，就避免了for loop循环上去的重复，

一般是递归过去一种，for loop一种，有duplicate就可以这样避免


```` 
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<Integer> list=new ArrayList<>();
        List<List<Integer>> result=new ArrayList<>();
        Arrays.sort(nums);
        bt(nums,result,list,0);
        
        return result;
    }
    
    private void bt(int[] nums,List<List<Integer>> res,
                              List<Integer> list,int index) {
      
        res.add(new ArrayList<>(list));
        for(int i=index;i<nums.length;i++){
            if(i>index && nums[i]==nums[i-1]) continue;
            list.add(nums[i]);
            bt(nums,res,list,i+1);
            list.remove(list.size()-1);
        }
    }
}
//这里的i>index保证了如果i=index，然后两个一样是可以加的（回溯的时候可以加），但是从for loop顺上去不可以加
````

