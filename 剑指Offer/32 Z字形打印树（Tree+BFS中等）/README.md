https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/

<img width="523" alt="Screen Shot 2022-02-22 at 9 50 11 AM" src="https://user-images.githubusercontent.com/59748598/155190105-cc7b135e-0ebc-4ec4-bcc5-3d5a1dfc0e51.png">

这道题就是充分利用bfs和linkedList的add First/addLast removeFirst/removeLast

![image](https://user-images.githubusercontent.com/59748598/155190275-4905f0ef-5196-4a9a-971b-bf9df4262af4.png)


queue就正常的addLast然后removeFirst

然后每一层的temp List都和上一层反着来，上一层addFirst下一层就addLast，反之亦然

记住是从第二层开始的

代码：
```` 
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        
        List<List<Integer>> res=new LinkedList<>();
        if(root==null) return res;
        //allow remove first/remove last
        LinkedList<TreeNode> queue=new LinkedList<>();
        queue.add(root);
        int size=1;
        boolean flag=true;// next time start at last
        while(!queue.isEmpty()){
            LinkedList<Integer> list=new LinkedList<>();
            int levelNum=0;
            // TreeNode temp=queue.pop();
            if(flag){ //next start from left
                for(int i=0;i<size;i++){
                    TreeNode node=queue.removeFirst();
                    list.addLast(node.val);
                    if(node.left!=null){
                        levelNum++;
                        queue.addLast(node.left);
                    }
                    if(node.right!=null){
                        levelNum++;
                        queue.addLast(node.right);
                    }
                }
            }
            else{
                for(int i=0;i<size;i++){
                    TreeNode node=queue.removeFirst();
                    list.addFirst(node.val);
                    if(node.left!=null){
                        levelNum++;
                        queue.addLast(node.left);
                    }
                    if(node.right!=null){
                        levelNum++;
                        queue.addLast(node.right);
                    }
                }
            }
            res.add(list);
            size=levelNum;
            flag=!flag;
            
        }
        return res;


    }
}
````




