https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/



<img width="614" alt="Screen Shot 2022-02-18 at 10 40 39 AM" src="https://user-images.githubusercontent.com/59748598/154743149-a2282988-26f6-4474-8a96-2bf6309beade.png">

这道题有一个坑，就是他的random实际上也是指向Node，不是index，打印出来可以看到，所有指向ramdom.val都是Node.val不是index

<img width="487" alt="Screen Shot 2022-02-18 at 10 42 08 AM" src="https://user-images.githubusercontent.com/59748598/154743323-86ef99ee-cb1a-4125-99e9-1988e02181a7.png">

用hashmap去存原来链表的节点->复制链表的节点

我的傻逼做法，先构建好next，每次next顺便存一下，回头random在loop一次查找 99%

```` 
class Solution {
    public Node copyRandomList(Node head) {
        if(head==null) return null;

        HashMap<Node,Node> map=new HashMap<>();
        Node cur1=head;
        Node root=new Node(cur1.val);
        Node copy=root;
        map.put(head,root);
        while(cur1.next!=null){
            copy.next=new Node(cur1.next.val);
            copy=copy.next;
            cur1=cur1.next;
            map.put(cur1,copy);
        }
        //build random
        cur1=head;
        copy=root;
        while(cur1!=null){
            copy.random=map.get(cur1.random);
            copy=copy.next;
            cur1=cur1.next;
        }
        return root;
    }
}
````

标准做法，先存好，loop map吧next和random同时处理了

```` 
class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node,Node> map=new HashMap<>();
        Node cur1=head;
        while(cur1!=null){
            map.put(cur1,new Node(cur1.val));
            cur1=cur1.next;
        }
        
        for(Map.Entry<Node,Node> entry :map.entrySet()){
            Node key=entry.getKey();
            Node next=map.get(key.next);
            Node random=map.get(key.random);
            if(next!=null && random !=null){
                //System.out.println("current is "+key.val+" next is "+next.val+"  random is "+random.val);
            }
            entry.getValue().next=next;
            entry.getValue().random=random;
        }
        return map.get(head);
    }
}
````





