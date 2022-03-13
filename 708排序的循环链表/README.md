https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/


<img width="523" alt="Screen Shot 2022-03-13 at 12 14 01 PM" src="https://user-images.githubusercontent.com/59748598/158075327-34d54639-50a0-42e3-8d6b-6a453e5c3523.png">

在本来就排序好的循环链表里找到合适的位置插入一个节点，如图所示如果插入2就找到1，插入0或者插入5就找到4


![image](https://user-images.githubusercontent.com/59748598/158075356-9872a8f7-8968-4d02-98fe-b072b76ca92c.png)

有两种情况，一种是正常递增的情况，即current.val<current.next.val,这个时候要找到1的情况局势insertVal>current.val && insertVal<current.next.val ,还是简单的就是插入的比当前大并且比后面小

然后因为可能有重复，所以全部大于小于都添加=号，这里发现添加=不影响逻辑，下面也是

 
```` 
if(current.val<=current.next.val){
                if(insertVal>=current.val && insertVal<=current.next.val){
                    break;
                }
}
````

另一种情况是从最大到最小（4->1）即current.val>current.next.val

这里current是最大值 current.next是最小值 （插入前）。 如果想插入5/0就要从这里下手  ，  上面的情况是找到5即insertVal>current.val (大于最大)，下面是小于最小

```` 
else{
                if(insertVal>=current.val){
                    break;
                }
                else if(insertVal<=current.next.val){
                    break;
                }
            }
````
之后找到current就把next变动就好了

完整代码

```` 
/*
// Definition for a Node.
class Node {
    public int val;
    public Node next;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _next) {
        val = _val;
        next = _next;
    }
};
*/

class Solution {
    public Node insert(Node head, int insertVal) {
        if(head == null) {
            Node newNode = new Node(insertVal);
            newNode.next = newNode;
            return newNode;
        }
        
        Node current=head;
        while(current.next!=head){
            if(current.val<=current.next.val){
                if(insertVal>=current.val && insertVal<=current.next.val){
                    break;
                }
            }
            //最大值到最小值这段过程 4->1
            else{
                if(insertVal>=current.val){
                    break;
                }
                else if(insertVal<=current.next.val){
                    break;
                }
            }
            
            current=current.next;
        }
        //current 后面
        Node next=current.next;
        Node insert=new Node(insertVal,next);
        current.next=insert;
        return head;
    }
}
````





