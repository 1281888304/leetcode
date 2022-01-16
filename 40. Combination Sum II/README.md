这道题和39一模一样，就是多了一个不能重复，给了重复数字，这里只需要加一个如果和上一个相等就跳过就好，不需要加visited数组，虽然这里也不让重复使用数字

但是可以通过i+1的方式，让他递归的时候不碰到上一次

```` 
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result=new ArrayList<>();
        List<Integer> list=new ArrayList<>();
        Arrays.sort(candidates);
        if(candidates.length<=0 || candidates==null){
            return result;
        }
        backtrack(0,list,result,candidates,target);
        return result;
    }
    
    private void backtrack(int start,List<Integer> list,
                          List<List<Integer>> result,int[] candidates,int target){
        if(target==0){
            result.add(new ArrayList<>(list));
            return;
        }
        // if(target-candidates[start]<0)
        //     return;
        for(int i=start;i<candidates.length;i++){
            if(i>start && candidates[i]==candidates[i-1]){
                continue;
            }
            if(target-candidates[i]<0)
                break;
            list.add(candidates[i]);
            backtrack(i+1,list,result,candidates,target-candidates[i]);
            list.remove(list.size()-1);
        }
    }
}
````

