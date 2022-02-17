就把图画出来，prev head cur next四个node来回操作，记得prev一开始永远是前面那个，所以最后prev要=head

![image](https://user-images.githubusercontent.com/59748598/154545615-907a5022-f0b6-4fbd-ad8d-36045cb64dff.png)

```` 
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev=null,cur=head;
        while(cur!=null){
            ListNode next=cur.next;
            //cur.next=null;
            cur.next=prev;
            head=cur;
            cur=next;
            prev=head;
        }

        return head;
    }
}
````








