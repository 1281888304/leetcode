https://leetcode-cn.com/problems/successor-lcci/

<img width="522" alt="Screen Shot 2022-04-05 at 10 27 24 AM" src="https://user-images.githubusercontent.com/59748598/161815017-50bc2075-7627-42e5-9826-6c301eafc1ae.png">


就是很简单，后面一个可以看成倒过来的prev，用inorder的顺序，先右在左就把顺序倒过来了，然后return的话，在主方法里完成比较简单

```` 
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    TreeNode prev=null;
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root==null){
            return null;
        }
        TreeNode left=inorderSuccessor(root.right,p);
        if(root==p){
            return prev;
        }
        prev=root;
        TreeNode right=inorderSuccessor(root.left,p);
        if(left==null && right==null){
            return null;
        }

        return left==null? right:left;
    }
}
````



