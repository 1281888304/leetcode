https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/

https://leetcode-cn.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/

<img width="539" alt="Screen Shot 2022-03-17 at 12 56 14 PM" src="https://user-images.githubusercontent.com/59748598/158884999-ad6dee3b-9e6f-4c88-8981-2f094caf0c2d.png">

<img width="535" alt="Screen Shot 2022-03-17 at 12 56 28 PM" src="https://user-images.githubusercontent.com/59748598/158885042-b0ccb257-e00e-4fb0-a747-8f66cdc56995.png">

根据BST得到一个链表，挂念就是利用inorder是排序好的这个原理 left=>root->right

然后左指数指向prev，right指向next

![image](https://user-images.githubusercontent.com/59748598/158885489-7be0207c-efbb-43ec-a56d-2d8e29747113.png)

遍历到1的时候，因为是第一个，把head设为1。  遍历到2的时候，，把1的right指向2，2的left指向1 至于2的next（right），到下一次的时候，利用prev来做

我们需要三个成员变量，prev head tail，但是loop到5的时候，prev就是tail尾巴，所以我们把tail去掉

代码：
```` 
class Solution {
    Node prev,head,tail;
    public Node treeToDoublyList(Node root) {
        if(root==null){
            return null;
        }
        dfs(root);
        //loop到最后prev=tail
        head.left=prev;
        prev.right=head;
        return head;
    }

    public void dfs(Node root){
        if(root==null) return;
        dfs(root.left);
        //inorder 操作
        //设定head,第一个到达的是head
        if(prev==null){
            head=root;
        }
        //如果不是第一个到达，通过上一个设定next（right）
        else if(prev!=null){
            prev.right=root;
        }
        //不管是不是第一个到达，更新prev，root.prev(left)
        root.left=prev;
        prev=root;


        dfs(root.right);
    }
}
//排序的循环双向链表
// inorder是按照顺序走的 left->root->right
//按照left是prev，right是next走
````







