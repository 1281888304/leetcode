基础版本，不需要实现从中间删除，用Node实现一个linkedlist

然后如果需要size，就在stack构造器实现加一个size。有个注意的地方是push的时候要判断是不是第一个

leetcode：155

代码：
```` 
class MinStack {
    Node head;
    //Node tail;

    public MinStack() {
        
    }
    
    public void push(int val) {
        if(head==null){
            head=new Node(val,val,null);
        }else{
            int min=Math.min(head.min,val);
            head=new Node(val,min,head);
        }
        
    }
    
    public void pop() {
        head=head.next;
        
    }
    //like peek
    public int top() {
        return head.val;
    }
    
    public int getMin() {
        return head.min;
        
    }
}

class Node{
    int val;
    int min;
    Node next;
    
    public Node(int val,int min,Node next){
        this.val=val;
        this.min=min;
        this.next=next;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
````




