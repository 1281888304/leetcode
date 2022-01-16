这道题的关键就是，比如是第一个拿了，第一个就不能拿第二次，但是这个有可以比如说[1,2,3], 答案可以是[3,2,1]，就不能用index/start方法，毕竟可以从后往前走

这就要加一个boolean数组，来确认哪个走过了，下一次就跳过，然后如果走失败了（在这里是找下一个答案），就撤销这个操作[1,2,3]先撤销3 在撤销 2的到[1]，然后1会顺着for loop把3加上

class Solution {

    public List<List<Integer>> permute(int[] nums) {
        int n=nums.length;
        List<List<Integer>> res=new ArrayList<>();
        List<Integer> list=new ArrayList<>();
        boolean[] visited=new boolean[n];
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


  递归之前 => [1]
  递归之前 => [1, 2]
  递归之前 => [1, 2, 3]
递归之后 => [1, 2]
递归之后 => [1]
  递归之前 => [1, 3]
  递归之前 => [1, 3, 2]
递归之后 => [1, 3]
递归之后 => [1]
递归之后 => []
  递归之前 => [2]
  递归之前 => [2, 1]
  递归之前 => [2, 1, 3]
递归之后 => [2, 1]
递归之后 => [2]
  递归之前 => [2, 3]
  递归之前 => [2, 3, 1]
递归之后 => [2, 3]
递归之后 => [2]
递归之后 => []
  递归之前 => [3]
  递归之前 => [3, 1]
  递归之前 => [3, 1, 2]
递归之后 => [3, 1]
递归之后 => [3]
  递归之前 => [3, 2]
  递归之前 => [3, 2, 1]
递归之后 => [3, 2]
递归之后 => [3]
递归之后 => []
输出 => [[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]

作者：liweiwei1419
链接：https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

