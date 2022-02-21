https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/

<img width="537" alt="Screen Shot 2022-02-21 at 11 22 05 AM" src="https://user-images.githubusercontent.com/59748598/155015432-dd8df2a6-ab52-4632-b704-c8b0c7cea2af.png">

这道题的目的就是找公共节点，然后不是void返回值的。可以通过寻找到p或者q来判断是否找到其中一个。

通过root来判断，

1 如果左边找到了其中一个并且右边也找到其中一个，拿父亲节点肯定就是root
2 如果左边右边都没找到，就返回null（递归的时候用）
3 如果左边没找到，右边找到了，那肯定都在右边，并且右边找到的那个肯定是父亲节点（通过递归重新走一遍判断）
4 右边没找到没左边找到了，同样道理

代码

```` 
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null) return null;
        if(root==p || root==q) return root;
        TreeNode left=lowestCommonAncestor(root.left,p,q);
        TreeNode right=lowestCommonAncestor(root.right,p,q);
        if(left== null && right==null) return null;
        else if(left==null && right!=null) return right;
        else if(left!=null && right==null) return left;
        else{
            return root;
        }

    }
}
````








