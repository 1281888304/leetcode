<img width="1342" alt="Screen Shot 2022-07-24 at 3 48 41 PM" src="https://user-images.githubusercontent.com/59748598/180668959-8a5ddc6a-37dd-41e8-ae68-9805b0214bb7.png">

核心就是最后prev成了head，head成了最后一个

然后制定链表反转运用的也是这一套

<img width="669" alt="Screen Shot 2022-07-24 at 3 49 24 PM" src="https://user-images.githubusercontent.com/59748598/180668977-31efa09b-d426-4f41-a49b-26b25803afb8.png">

线断开left right，然后就是在最后pre.next=right

left.next=cur连起来


```` 
import java.util.*;

/*
 * public class ListNode {
 *   int val;
 *   ListNode next = null;
 * }
 */

public class Solution {
    /**
     * 
     * @param head ListNode类 
     * @param m int整型 
     * @param n int整型 
     * @return ListNode类
     */
    public ListNode reverseBetween (ListNode head, int m, int n) {
        // write code here
        ListNode dummy=new ListNode(-1);
        dummy.next=head;
        ListNode pre=dummy;
        for(int i=1;i<m;i++){
            pre=pre.next;
            
        }
        ListNode right=pre;
        for(int i=0;i<n-m+1;i++){
            right=right.next;
        }
        ListNode left=pre.next;
        ListNode cur=right.next;
        
        pre.next=null;
        right.next=null;
        
        pre.next=reverse(left);
        
        left.next=cur;
        return dummy.next;

    }
    
    public ListNode reverse(ListNode head) {
        ListNode prev=null;
        ListNode cur=head;
        while(cur!=null){
            ListNode next=cur.next;
            cur.next=prev;
            prev=cur;
            cur=next;
            //head=cur;
        }
        return prev;

    }
}
````
