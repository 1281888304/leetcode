https://leetcode-cn.com/problems/successor-lcci/

<img width="522" alt="Screen Shot 2022-04-05 at 10 27 24 AM" src="https://user-images.githubusercontent.com/59748598/161815017-50bc2075-7627-42e5-9826-6c301eafc1ae.png">


就是很简单，后面一个可以看成倒过来的prev，用inorder的顺序，先右在左就把顺序倒过来了，然后return的话，在主方法里完成比较简单.升级版就是不浪费时间通过对比root和p的大小

- 如果根节点小于或等于要查找的节点p, 直接进入右子树递归
- 如果根节点大于要查找的节点, 则暂存左子树递归查找的结果,
    - 如果是 null, 说明在该根节点的左子树中没找到比p大的节点，也就说明该根节点就是要找的p的后继，则直接返回当前根节点;
    - 如果不是 null,说明找到了答案，返回左子树递归查找的结果  


升级版代码：
```` 
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root==null || p==null){
            return null;
        }
        if(root.val<=p.val){
            TreeNode right = inorderSuccessor(root.right,p);
            return right;
        }else{
            TreeNode left= inorderSuccessor(root.left,p);
            return (left!=null)?left:root;
        }

    }
}


````


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



