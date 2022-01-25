![image](https://user-images.githubusercontent.com/59748598/150937547-7872db5f-3237-4621-b72f-c2cfc2084d5d.png)

inorder left->Node->right

inorder就是不停的往左，直到null就返回上一层，用while loop不停的往左走，直到null，null是不放进stack里的

添加过程就是先添加temp，然后让temp=temp.left;  然后下一步继续添加left直到null，然后让temp=temp.right; 下一步就找temp.right这个node的最左边


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
    private List<Integer> list=new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        
        List<Integer> result=new ArrayList<>();
        
        if(root==null) return result;
        
        inorder(root,result);
        return result;
      
        
    }
    
    private void inorder(TreeNode root,List<Integer> res){
        Deque<TreeNode> stack=new LinkedList<>();
        TreeNode temp=root;
        while(!stack.isEmpty() || temp!=null){
            while(temp!=null){
                stack.push(temp);
                temp=temp.left;
            }
            temp=stack.pop();
            res.add(temp.val);
            temp=temp.right;
        }
    }

    private void inorder2(TreeNode root){
        if(root==null){
            return;
        }        
        inorder2(root.left);
        list.add(root.val);
        inorder2(root.right);        
    }

}
````




