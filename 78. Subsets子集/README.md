就很简单的子集合，什么都加，出口直接加不需要return，等他自己for loop走完了return，用index/boolean数组都可以避免


```` 
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list=new ArrayList<>();
        List<List<Integer>> result=new ArrayList<>();
        
        bt(nums,result,list,0);
        
        return result;
    }
    //不能从后往前加，需要index，比如说不能312 132
    private void bt(int[] nums,List<List<Integer>> res,List<Integer> list,
                   int index){
        //这里没什么出口，啥都加，就是不能倒着加，回溯通过for loop走完的方式加
        res.add(new ArrayList<>(list)); 
        for(int i=index;i<nums.length;i++){
            list.add(nums[i]);
            bt(nums,res,list,i+1);
            list.remove(list.size()-1);
        }
    }
}

//use remove to go foward the others
            // like [1,2,3]
            //remove 3, and remove 2 and remove 1
            //goes to [2] and then [2,3]
            //and then remove3 ,and remove 2
            //and goes [3]


````


