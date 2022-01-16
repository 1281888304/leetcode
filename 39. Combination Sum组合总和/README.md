<img width="629" alt="Screen Shot 2022-01-15 at 8 14 34 PM" src="https://user-images.githubusercontent.com/59748598/149647063-9cc73a9f-8d30-4b6e-8f1b-b9e1ade358a3.png">
这道题的关键在于index，index在回溯里面的作用，就是为了不回头去加他，为什么不是index+1，因为每个数字可以重复使用

比如说[2,3,5,6,7].  key=7. 我们可以2+2+3 但是如果没有index，那么for loop从0开始，那样的话，3可以加2这是题目不允许的

for loop是在反复需要同一个数字多个答案的时候用的

把target不停地减小，如果target刚好等于0，return并且加到list 里，如果target可能变成负数，就不要继续往下走了

切记不是增加，减小可以有一个得到负数的可能，增加操作太麻烦

```` 
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result=new ArrayList<>();
        List<Integer> list=new ArrayList<>();
        Arrays.sort(candidates);
        if(candidates.length<=0 || candidates==null){
            return result;
        }
        bt(result,list,candidates,target,0);
        return result;
    }
    //可以重复循环，用for loop
    //把target不停地减小，如果target刚好等于0，return并且加到list 里
    //如果target可能变成负数，就不要继续往下走了
    private void bt(List<List<Integer>> res,List<Integer> list,
                    int[] candidates,int target,int index){
        if(target==0){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i=index;i<candidates.length;i++){
            //可能变成负数，return，因为sort过，往后走也没意义
            if(target<candidates[i]){
                return;
            }
            list.add(candidates[i]);
            bt(res,list,candidates,target-candidates[i],i);
            //走成功或者不成功都回来撤销操作，尝试下一个
            list.remove(list.size()-1);
        }
    }

}
//为什么要index，这里的index是不让往前加
````


