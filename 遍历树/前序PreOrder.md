

<img width="599" alt="Screen Shot 2022-01-24 at 11 45 31 PM" src="https://user-images.githubusercontent.com/59748598/150933419-7a7a8586-1620-40ae-9e8c-b64bba8a4af5.png">

![image](https://user-images.githubusercontent.com/59748598/150933743-74bc6c79-53f1-49bb-b8d5-c234162e9b9f.png)


preOrder前序就是上到左下，先把root放进去，res加root.val然后看看左右为不为空，不为就加。注意先加右边，因为stack先加后出，我们先要左边所以后加

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
    public List<Integer> preorderTraversal(TreeNode root) {
        
        List<Integer> list=new ArrayList<>();
        if(root==null) return list;
        preOrder(root,list);
        return list;
    }
    
    
    
    private void preOrder(TreeNode root,List<Integer> res){
        Deque<TreeNode> stack=new LinkedList<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode temp=stack.pop();
            res.add(temp.val);
            if(temp.right!=null){
                stack.push(temp.right);
            }
            if(temp.left!=null){
                stack.push(temp.left);
            }
            
        }
    }
    
    private void traversal(TreeNode root,List<Integer> list){
        if(root==null){
            return;
        }
        
        list.add(root.val);
        traversal(root.left,list);
        traversal(root.right,list);
    }
}
````





