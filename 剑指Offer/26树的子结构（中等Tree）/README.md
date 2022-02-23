https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/

<img width="540" alt="Screen Shot 2022-02-23 at 10 15 36 AM" src="https://user-images.githubusercontent.com/59748598/155381733-15b59507-1e63-446b-b186-63515820deb6.png">

这道题有一个问题，就是包含，和可能会有重复数值的节点（两个node的value都是4），所以说不能通过找到某一个节点，再去判断是否包含，要loop 每一个节点

通过题目给的主方法loop每一个节点的的代码，判断都不等于null，然后每一个节点每一个节点的判断是否包含：
```` 
public boolean isSubStructure(TreeNode A, TreeNode B) {
        return (A!=null && B!=null) &&
            (contains(A,B) || isSubStructure(A.left,B) || isSubStructure(A.right,B));
    }
````

关于包含的代码：
我自己的长版本：
```` 
private boolean contain(TreeNode A,TreeNode B){
        if(A==null && B==null) return true;
        if(A!=null && B==null) return true;
        if(A==null && B!=null) return false;
        
        if(A.val != B.val) return false;
        return contain(A.left,B.left) &&
            contain(A.right,B.right);

    }
````
大佬的简化版本：B==null的时候，不管A和B是否是null都是true，A==null第二行，B肯定不是null（上一行判断过了），所以返回false

```` 
private boolean contains(TreeNode A,TreeNode B){
        if(B==null) return true;
        if(A==null) return false;
        if(A.val!=B.val) return false;
        return contains(A.left,B.left) && contains(A.right,B.right);
    }
````


完整代码：
```` 
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        return (A!=null && B!=null) &&
            (contains(A,B) || isSubStructure(A.left,B) || isSubStructure(A.right,B));
    }

    private boolean contains(TreeNode A,TreeNode B){
        if(B==null) return true;
        if(A==null) return false;
        if(A.val!=B.val) return false;
        return contains(A.left,B.left) && contains(A.right,B.right);
    }


}
````







