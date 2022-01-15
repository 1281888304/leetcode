




<img width="605" alt="Screen Shot 2022-01-14 at 11 37 03 PM" src="https://user-images.githubusercontent.com/59748598/149613853-2ad7756a-8a67-42b5-8f75-83adcbd07d33.png">

这道题的精髓在于删掉以后桥接回去，往后走一步，找最左边的，这样才能刚刚好的卡在这个平衡，找到替换的，把需要删除的换成这个找到的数字，然后在root.right“删除找到的这个数”

因为最后要返回root，导致要root.left=和root.right等于，不能直接把root改变


```` 
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root==null) return null;
        //往右走
        if(root.val<key){
            root.right=deleteNode(root.right,key);
        }
        else if(root.val>key){
            root.left=deleteNode(root.left,key);
        }
        //root.val == key
        else{
            //最简单的状态，两边都为空，直接为空删除
            if(root.left==null && root.right==null){
               root=null;
               
            }
            else if(root.left!=null && root.right==null){
                root=root.left;
            }
            else if(root.right!=null && root.left==null){
                root=root.right;
            }
            else{
                root.val=findSuccessor(root);
                root.right=deleteNode(root.right,root.val);
            }
   
        }
        return root;
    }
    
    //往右走一步，然后不停的向左走找到能找到最左边的
    //因为只有最左边的才能刚好替换掉
    private int findSuccessor(TreeNode root){
        root=root.right;
        while(root.left!=null){
            root=root.left;
        }
        return root.val;
    }
}



````


