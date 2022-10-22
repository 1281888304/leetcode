写在开头：面试官您好，是这样我这个肯定不是最优的解法，只是简单的用了bfs+dfs实现的。我网上看了一些解法，很巧妙，但是不是我的，我想展示一个我平常笔试/面试手撕代码的一个代码水平，

这段代码是我暂时能够最快想出来的一个实现算法，如果未来有时间我会继续尝试学习网上的优秀写法，但是确实是不想作弊，所以就用了一些笨重的解法

实现逻辑就是普通的bfs构建树，然后dfs每次遍历的时候解决一层的竞争，还是希望给个贵司给个机会，谢谢

```` 
package aozhe;


import java.util.LinkedList;


public class SortByBinaryTree {

  public static void main(String[] args) {

    int[] arr = new int[]{8, 6, 7, 3, 1, 2, 5, 4};
    TreeNode root = buildTree(arr);
    System.out.println("锦标赛排序前");
    printHelper(root);
    System.out.println("排序后");
    TreeNode rootAfterSort=sort(root);
    printHelper(rootAfterSort);
  }

  //
  public static TreeNode sort(TreeNode root){
    while(root.val==-1){
      dfs(root);
    }
    return root;
  }

  //每次dfs做一次
  public static void dfs(TreeNode root){
    if(root==null){
      return;
    }
    if(root.left.val!=-1 && root.right.val!=-1){
      root.val=Math.max(root.left.val,root.right.val);
      return;
    }
    dfs(root.left);
    dfs(root.right);
  }



  // 固定arr.length>=2 && arr.length%2==0
  public static TreeNode buildTree(int[] arr) {
    int k = arr.length;
    int depth = 0;
    while (k != 1) {
      depth++;
      k /= 2;
    }
    //一共k层
    TreeNode root = new TreeNode(-1);
    //用bfs实现构造数
    int level = 0;
    LinkedList<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (level < depth-1) {
      level++;
      int size = queue.size();
      for (int i = 0; i < size; i++) {
        TreeNode temp = queue.poll();
        temp.left = new TreeNode(-1);
        temp.right = new TreeNode(-1);
        queue.offer(temp.left);
        queue.offer(temp.right);
      }

    }
    //最底层
    for (int i = 0; i < arr.length; i += 2) {
      TreeNode temp = queue.poll();
      temp.left = new TreeNode(arr[i]);
      temp.right = new TreeNode(arr[i + 1]);
    }
    return root;
  }

  //bfs便利树查看锦标赛情况
  public static void printHelper(TreeNode root) {
    LinkedList<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
      int size = queue.size();
      for (int i = 0; i < size; i++) {
        TreeNode temp = queue.poll();
        System.out.print(temp.val + "  ");
        if (temp.left != null) {
          queue.offer(temp.left);
        }
        if (temp.right != null) {
          queue.offer(temp.right);
        }
      }
      System.out.println();
    }
  }


}


class TreeNode {

  public int val;
  public TreeNode left;
  public TreeNode right;

  public TreeNode(int val) {
    this.val=val;
  }

}

````

<img width="401" alt="Screen Shot 2022-10-21 at 10 34 10 PM" src="https://user-images.githubusercontent.com/59748598/197322453-dc180f10-3526-4b56-9dd3-57d5ab48d063.png">



