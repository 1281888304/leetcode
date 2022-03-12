https://leetcode-cn.com/problems/hPov7L/


<img width="451" alt="Screen Shot 2022-03-11 at 7 29 43 PM" src="https://user-images.githubusercontent.com/59748598/158002062-b2b64b40-3ded-4443-963a-230683b481c4.png">

比较简单，用bfs每层装进去之前判断一个最大就好，不要用TreeSet.last();很慢

```` 
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        if(root==null) return res;
        LinkedList<TreeNode> queue=new LinkedList<>();
        queue.offer(root);
        int size=1;
        
        while(!queue.isEmpty()){
            int curSize=0;
            int max=Integer.MIN_VALUE;
            for(int i=0;i<size;i++){
                TreeNode temp=queue.pop();
                max=Math.max(temp.val,max);
                if(temp.left!=null){
                    queue.offer(temp.left);
                    curSize++;
                }
                if(temp.right!=null){
                    queue.offer(temp.right);
                    curSize++;
                }
            }
            res.add(max);
            size=curSize;
            
        }
        return res;

    }
}
````



