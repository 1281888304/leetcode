https://leetcode-cn.com/problems/lMSNwu/

<img width="397" alt="Screen Shot 2022-02-17 at 10 12 54 AM" src="https://user-images.githubusercontent.com/59748598/154544504-806ab815-02c0-47f0-95e1-b8247bd1efaa.png">

一般就用反转在相加，但是这里不让，所以直接就用stack的方式来做，先进后取出来

stack慢，用list反着读取就是stack

精妙就在于 res=new ListNode(val,res);可以反着创建node然后指向自己，不能分开，一分开res.next=res;肯定就不行了

 
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        List<Integer> list1=new ArrayList<>();
        List<Integer> list2=new ArrayList<>();

        while(l1!=null){
            list1.add(l1.val);
            l1=l1.next;
        }

        while(l2!=null){
            list2.add(l2.val);
            l2=l2.next;
        }

        ListNode res=null;
        int index1=list1.size()-1;
        int index2=list2.size()-1;
        boolean carry=false;
        while(index1>=0 || index2>=0){
            int n1=index1>=0 ? list1.get(index1--) :0;
            int n2=index2>=0 ? list2.get(index2--) :0; 
            int sum=n1+n2+(carry?1:0);
            res=new ListNode(sum%10,res);//指向自己,不能分开，分开就不行了
            carry=(sum>=10) ? true:false;
            
        }
        if(carry) res=new ListNode(1,res);
        return res;



    }
}
````


