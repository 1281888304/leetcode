就是把每个node的next指针设置好

<img width="613" alt="Screen Shot 2022-02-14 at 8 08 34 PM" src="https://user-images.githubusercontent.com/59748598/153991019-a8b8ad64-e1a9-4d32-aead-b413b7f1789e.png">

这里我们一层层来，每层设置完，就到下一层最左边的

所以要用两个while loop，外面那层控制一层层来，里面那个把这一层所有的node的next指针都设置好

有一个关键的是在findNext，通过parent节点去找next，比如说我们在2，需要通过1去找3 （2就是current.left）用current去找3

这里如果直接找下一个的话，需要在next level那里判断head.right

```` 
private Node findNext(Node prev){
        if(prev.next==null)
            return null;
        Node cur=prev;
        while(cur!=null){
            cur=cur.next;
            if(cur.left!=null) return cur.left;
                
            if(cur.right!=null)  return cur.right;
            
        }
        return null;
    }
````

完整代码：


```` 
class Solution {
    public Node connect(Node root) {
        if(root==null) return null;
        
        Node head=root;
        while(head!=null){
            Node current=head;
            while(current!=null){
                if(current.left!=null && current.right!=null){
                    current.left.next=current.right;
                    current.right.next=findNext(current.next);
                }
                if(current.left!=null && current.right==null){
                    current.left.next=findNext(current.next);
                }
                if(current.left==null && current.right!=null){
                    current.right.next=findNext(current.next);
                }
                
                current=current.next;
            }
            if(head.left!=null)
                head=head.left;
            else{
                Node nextLineStart=findNext(head);
                head=nextLineStart;
            }
        }
        return root;
    }
    
    
    private Node findNext(Node current){
        if(current==null)
            return null;
        if(current.left!=null){
            return current.left;
        }
        if(current.right!=null){
            return current.right;
        }
        //now all is null
        return findNext(current.next);
    } 
}
````

findNext用while
```` 
class Solution {
    public Node connect(Node root) {
        if(root==null) return null;
        
        Node head=root;
        while(head!=null){
            Node current=head;
            while(current!=null){
                if(current.left!=null && current.right!=null){
                    current.left.next=current.right;
                    current.right.next=findNext(current);
                }
                if(current.left!=null && current.right==null){
                    current.left.next=findNext(current);
                }
                if(current.left==null && current.right!=null){
                    current.right.next=findNext(current);
                }
                
                current=current.next;
            }
            if(head.left!=null)
                head=head.left;
            else if(head.right!=null)
                head=head.right;
            else{
                Node nextLineStart=findNext(head);
                head=nextLineStart;
            }
        }
        return root;
    }
    
    private Node findNext(Node prev){
        if(prev.next==null)
            return null;
        Node cur=prev;
        while(cur.next!=null){
            cur=cur.next;
            if(cur.left!=null) return cur.left;
                
            if(cur.right!=null)  return cur.right;
            
        }
        return null;
    }

}
````



