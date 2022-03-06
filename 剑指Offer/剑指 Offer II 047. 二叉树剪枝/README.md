https://leetcode-cn.com/problems/pOCWxh/

<img width="529" alt="Screen Shot 2022-03-05 at 5 50 38 PM" src="https://user-images.githubusercontent.com/59748598/156905775-4d018dbb-d42b-4d9a-beea-5dafebb1f28c.png">

这道题的中心思想就是把root=0且全部分支为0的set null

慵懒的版本：用helper的boolean来查看是否全部都是0，然后一个个loop
```` 
class Solution {
    public TreeNode pruneTree(TreeNode root) {
        if(helper(root)){
            return null;
        }
        if(root==null) return null;
        if(helper(root.left)){
            root.left=null;
        }
        if(helper(root.right)){
            root.right=null;
        }
        TreeNode left=pruneTree(root.left);
        TreeNode right=pruneTree(root.right);
        return root;
    }
    //check if all 0
    public boolean helper(TreeNode root){
        if(root==null) return true;
        if(root.val==1) return false;
        return helper(root.left) 
            && helper(root.right);
    }
}
````

简洁版本，先把root root.left root.right拿出来，在看root是否是0，left right是否是null（如果符合条件，在递归到这一步的时候，就已经是null了）

post order后序角度从loop到最下面的时候，单个节点等于0会直接return null，然后一步步往上把所有单个节点=0都设 null（最下面的变成null了，从下面往上剪）



```` 
class Solution {
    public TreeNode pruneTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        root.left = pruneTree(root.left);
        root.right = pruneTree(root.right);
        if (root.val == 0 && root.left == null && root.right == null) {
            return null;
        }
        return root;
    }

}
````






