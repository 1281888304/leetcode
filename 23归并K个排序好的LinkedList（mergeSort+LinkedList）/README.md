这道题精髓在于和以往的int array 归并（merge）排序不同，这次通过return不停的把ListNode 数组array的element归并在一起，到了最后返回一个ListNode head


<img width="723" alt="Screen Shot 2022-02-04 at 5 20 57 PM" src="https://user-images.githubusercontent.com/59748598/152623226-53f8be39-fccb-41e6-bebe-2e4ab745e831.png">

如图所示，两两合并。 合并到最后就有就返回一个result

然后另外一个就是merge两个ListNode的时候，不再用往常的遍历方法，用了递归

l1.next=mergeTwoListNode(l2,l1.next);
return l1;

很精妙

正常遍历的时候也要注意一个问题，如果是current作为Dummy.next的话，current就算赋值了，也连不上dummy。

原因是这样的，如果暂时下一个为null，就最好不要动，有了current/prev .next=下一个对象，如果dummy.next=head没问题，构建了连接

dummy.next=null的时候，current = dummy.next这个时候current是null，不是ListNode，current并没有指向dummy.next,而是指向了null

```` 
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
   public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        return merge(lists, 0, lists.length - 1);
    }

    //+1是为了避免当到了最后，left =right，-1的话right变成left-1
    private ListNode merge(ListNode[] lists, int left, int right) {
        if(left==right) return lists[left];
        int mid=left+(right-left)/2;
        ListNode leftPart=merge(lists,left,mid);
        ListNode rightPart=merge(lists,mid+1,right);
        return mergeTwoLists(leftPart,rightPart);
    }
    

    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        //ListNode head=new ListNode(-1);
        if(l1.val<l2.val){
            l1.next=(mergeTwoLists(l1.next,l2));
            return l1;
            
        }else{
            l2.next=(mergeTwoLists(l1,l2.next));
            return l2;
        }
    }


    
    // //题目给定了两个listNode长度是一样的，很简单
//     private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
//         if(l1==null) return l2;
//         if(l2==null) return l1;
//         ListNode dummy=new ListNode(-1);
//         ListNode prev=dummy;
//         while(l1 != null && l2!=null){
            
//             if(l1.val<l2.val){
//                 prev.next=l1;
//                 l1=l1.next;
//                 prev=prev.next;
//             }else{
//                 prev.next=l2;
//                 l2=l2.next;
//                 prev=prev.next;
//             }
//         }
//         prev.next=(l1==null) ? l2:l1;
//         return dummy.next;
//     }
}

//current是null的时候要new



````



