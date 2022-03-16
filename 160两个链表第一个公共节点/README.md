https://leetcode.com/problems/intersection-of-two-linked-lists/

<img width="500" alt="Screen Shot 2022-03-16 at 12 00 11 PM" src="https://user-images.githubusercontent.com/59748598/158666746-336810d5-a2d1-461f-a3e4-ffbcb9389f23.png">

![image](https://user-images.githubusercontent.com/59748598/158667562-f5437d52-fc69-49d3-acb8-17d508efc48f.png)

算法就是当一个链表遍历完了，就去遍历下一个链表。就算没有交叉，也能在某一刻同时便利到null

这个某一刻就是第二次。 可以看成把两个链表合在一起，p1/p2遍历到对方链表的时候，肯定会想交。因为看成两张链表合在一起的话是一样长的

用算法让他遍历完自己就去遍历别人

```` 
ListNode p1=headA;
        ListNode p2=headB;
        while(p1 !=p2){
            p1= p1==null ? headB : p1.next;
            p2= p2==null ?headA : p2.next;
            
        }
        return p2;
````





