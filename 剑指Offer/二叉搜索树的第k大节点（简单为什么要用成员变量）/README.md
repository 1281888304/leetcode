https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/

通过二叉树inorder中序可以判断 left->root->right是从最小的到最大的，反着来 right->root->left就是最大的到最小的

但是不能在递归的时候k-1,因为我们要找第k大的，如果递归的时候k-1，在返回上一层的时候，k-1这个指令就撤销了，比如说在下面代码里面，我们比如在left那里k往下递归确实-1了，但是回来的时候，k就变回参数里穿的那个
，在right那一行的k和root left那一行没有➖1的k是一样的，所以要使用成员变量

```` 
private void helper(TreeNode root,int k){
  //业务
  helper(root.left,k-1);
  //业务
  helper(root.right,k-1);
}
````


代码：
```` 
class Solution {
    int res,k;
    public int kthLargest(TreeNode root, int k) {
        this.k=k;
        if(root==null) return 0;
        
        dfs(root);
        return res;
    }

    void dfs(TreeNode root) {
        if(root == null) return;
        dfs(root.right);
        
        k--;
        if(k == 0) res = root.val;
        dfs(root.left);
    }


}
````






