<img width="538" alt="Screen Shot 2022-02-16 at 1 13 29 PM" src="https://user-images.githubusercontent.com/59748598/154358119-5e2a4ed6-a30e-453a-9afe-6d771ea1cd01.png">

题目给了pre Order和inORder两个数组我们可以用，pre order是 root -> left ->right;  in order : left->root->right

可以划分成
![image](https://user-images.githubusercontent.com/59748598/154358370-f61bb86d-2138-401e-aa61-02db98d6d2f3.png)

left/right意味着一个inner array数组

好比如说题目给的这个树，我们可以根据pre Order找到root，然后通过in order划分成[左边数组,   root,  右边数组 ]的方式分治的方法做这个题目，和merge sort很像，分治到单独的root在一个个结合起来

不要用arrays copy做成小数组，可能会左右不行，这种inner array数组的问题都通过index去做

用一个map存折in order数组的顺序，会帮助我们更快的找到在inorder数组里root index来更好的区分左边，右边

中间那个pre left == pre right有没有都无所谓，毕竟没有继续往下走也就是返回null，一样的，只不过快一丢丢

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length<=0 || inorder.length<=0) return null;
        
        Map<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<inorder.length;i++){
            map.put(inorder[i],i);
        }
        int n=preorder.length;

        return helper(preorder,inorder,0,n-1,0,n-1,map);
    }

    private TreeNode helper(int[] preorder, int[] inorder,int preLeft,int preRight,
    int inLeft,int inRight,Map<Integer,Integer> map){
        if(preLeft>preRight) return null;

        // if(preLeft==preRight){
        //     return new TreeNode(preorder[preLeft]);
        // }

        //左边第一个是pre left
        TreeNode root=new TreeNode(preorder[preLeft]);
        //找到index在inorder 数组所在的位子
        int rootIndex=map.get(root.val);

        int leftSize=rootIndex-inLeft;

        root.left=helper(preorder,inorder,preLeft+1,preLeft+leftSize,inLeft,rootIndex-1,map);
        root.right=helper(preorder,inorder,preLeft+leftSize+1,preRight,rootIndex+1,inRight,map);
        return root;
    }

//通过left right获得新的array数组，有点类似于merge，分到最后root只剩下一个一个这样返回在组合，分治
    
}


//帮左边/右边找到新的preOrder数组和新的inorder数组，分割点是root

````




