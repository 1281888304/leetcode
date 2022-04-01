https://leetcode-cn.com/problems/w6cpku/

<img width="548" alt="Screen Shot 2022-04-01 at 10 57 51 AM" src="https://user-images.githubusercontent.com/59748598/161317169-10910e61-10f9-4fd0-b730-9babd9f2e509.png">


<img width="560" alt="Screen Shot 2022-04-01 at 10 58 06 AM" src="https://user-images.githubusercontent.com/59748598/161317214-6988a737-24ff-4adc-94dd-9dfe56600a8d.png">

利用inorder的反着来，从大到小，先right后left，一路加上去

```` 
class Solution {
    int sum = 0;
    public TreeNode convertBST(TreeNode root) {
        dfs(root);
        return root;
    }
    private void dfs(TreeNode root){
        if(root == null) return;
        dfs(root.right);
        sum += root.val;
        root.val = sum;
        dfs(root.left);
    }
}

````

```` 
class Solution {
    int sum=0;
    public TreeNode convertBST(TreeNode root) {
        if(root!=null){
            convertBST(root.right);
            
            sum+=root.val;
            root.val=sum;
            convertBST(root.left);
        }
        return root;
    }
}
````


