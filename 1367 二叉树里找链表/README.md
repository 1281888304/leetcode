https://leetcode.com/problems/linked-list-in-binary-tree/

<img width="594" alt="Screen Shot 2022-03-17 at 1 35 37 PM" src="https://user-images.githubusercontent.com/59748598/158890743-c780e136-8250-441d-a505-0fe8c7e4730a.png">

在二叉树里找链表，和leetcode剑指offer26很像，只不过那个要求完全一样，这边可以像图上2->6不行，2->8可以，所以最后返回的时候用或|| 不是和 &&

首先方法都一样，每个节点每个节点查找，并且因为空不算，所以保证root不能是null
```` 
if(head==null)
            return true;
        return ( root!=null) && (contains(head,root) 
                                        || isSubPath(head,root.left)
                                        || isSubPath(head,root.right));
````

然后写contains方法，如果链表刚好到null，就最后一位，返回true

如果root不是null，这个时候链表不是null（上面判断过），返回false，值不一样也返回false

```` 
public boolean contains(ListNode head,TreeNode root){
        //链表刚好到null，就最后一位，返回true
        if(head==null)
            return true;
        //root不是null，这个时候链表不是null（上面判断过），返回false
        if(root==null)
            return false;
        if(head.val!=root.val)
            return false;
````

最后是递归部分，因为2到6不行，到8可以，所以用或||饭回来如果6返回的事false，8返回的是true，仍然返回true
```` 
public boolean contains(ListNode head,TreeNode root){
        //链表刚好到null，就最后一位，返回true
        if(head==null)
            return true;
        //root不是null，这个时候链表不是null（上面判断过），返回false
        if(root==null)
            return false;
        if(head.val!=root.val)
            return false;
        return contains(head.next,root.left)
        || contains(head.next,root.right);
    }
````

完整代码：

```` 
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    //check each point in root
    public boolean isSubPath(ListNode head, TreeNode root) {
        if(head==null)
            return true;
        return ( root!=null) && (contains(head,root) 
                                        || isSubPath(head,root.left)
                                        || isSubPath(head,root.right));
    }
    
    public boolean contains(ListNode head,TreeNode root){
        //链表刚好到null，就最后一位，返回true
        if(head==null)
            return true;
        //root不是null，这个时候链表不是null（上面判断过），返回false
        if(root==null)
            return false;
        if(head.val!=root.val)
            return false;
        return contains(head.next,root.left)
        || contains(head.next,root.right);
    }
}
````





