https://leetcode-cn.com/problems/LGjMqU/

<img width="488" alt="Screen Shot 2022-02-17 at 11 12 14 AM" src="https://user-images.githubusercontent.com/59748598/154553643-2ef29cbd-92cd-4010-a0e9-8c265cd4fd13.png">

首先用快慢指针找到中点，然后切断两边，把后面的反转，在一个个加就好了

我们知道快慢指针如果是 1->2->3->4分割成 1->2 :   3->4 或者1->2->3->4->5分割成1->2->3 : 4->5

所以是可行的，偶数mid就是前面那个，奇数mid就是正好中间

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
class Solution {
    public void reorderList(ListNode head) {
        //用快慢指针找到中间
        ListNode mid=head,fast=head;
        while(fast.next!=null && fast.next.next!=null){
            fast=fast.next.next;
            mid=mid.next;
        }
        ListNode secondPart=mid.next;
        mid.next=null;
        secondPart=reverse(secondPart);
        ListNode dummy=new ListNode(-1);
        ListNode current=dummy;
        while(head!=null && secondPart!=null){
            current.next=head;
            head=head.next;
            current=current.next;
            current.next=secondPart;
            secondPart=secondPart.next;
            current=current.next;
        }
        current.next=head==null? null : head;
        head=dummy.next;

    }

    private ListNode reverse(ListNode head){
        ListNode prev=null,cur=head;
        while(cur!=null){
            ListNode next=cur.next;
            cur.next=prev;
            head=cur;
            cur=next;
            prev=head;

        }
        return head;
    }
}
````



