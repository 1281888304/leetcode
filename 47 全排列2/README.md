这题是46升级版，多了一个有重复数字，所以我们要先把他sort了，然后判断，如果和前面一样就跳过

至于为什么跳过

这道题的精髓在于，如果那个continue，那么从第一个开始的回溯永远不会得到结果，只能从第二个开始才能得到结果，因为第二个可以反向回去加第一个，第一个不可以加第二个

[1,1,2]如果从第一个1开始的话，我们得不到答案，因为[1,2]这个时候已经没了，但是我们必须跳过第二个，不停的撤销到空数组[]然后从第二个1开始[1]=>[1,1]=>[1,1,2]

必须从第二个1开始才可以,注意上面第一个1是来自第二个，第二个1是来自第一个

class Solution {

    public List<List<Integer>> permuteUnique(int[] nums) {
        int n=nums.length;
        Arrays.sort(nums);
        List<List<Integer>> res=new ArrayList<>();
        List<Integer> list=new ArrayList<>();
        boolean[] visited=new boolean[nums.length];
        Arrays.fill(visited,false);
        
        bt(res,list,nums,visited);
        return res;
    }
    
    private void bt(List<List<Integer>> res,List<Integer> list,int[] nums,
                   boolean[] visited){
        //出口
        if(list.size()==nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        
        for(int i=0;i<nums.length;i++){
            if(i>0 && nums[i]==nums[i-1] && visited[i-1])
                continue;
            if(!visited[i]){
                visited[i]=true;
                list.add(nums[i]);
                bt(res,list,nums,visited);
                visited[i]=false;
                list.remove(list.size()-1);
            }
        }
        
    }
    
}


