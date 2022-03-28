https://leetcode-cn.com/problems/lru-cache/solution/lruhuan-cun-ji-zhi-by-leetcode-solution/

leetcode 146，还是写double linkedlist，这里最好用HashMap记录，不用的话能跑过20/22

题目让我们把最后使用的删掉，也就是头节点，尾巴节点，每次使用（get/put）就move到头节点，然后超过容量（capacity）就删掉尾巴tail，tail是最不使用的

这里为了避免null，用伪装节点来设置head tail

![Screen Shot 2022-03-28 at 12 12 03 PM](https://user-images.githubusercontent.com/59748598/160469713-b2233ae3-df46-4ace-8bcf-5f8709cef6ad.png)

然后往里面走，头节点就是head.next,尾巴tail就是tail.prev

代码实现：Node里设一个啥都没有的空构造器，可以new但是不设置任何参数
```` 
private class Node{
        int key;
        int val;
        Node next;
        Node prev;
        
        public Node(int _key,int _val,Node _next,Node _prev){
            this.key=_key;
            this.val=_val;
            this.next=_next;
            this.prev=_prev;
        }
        
        public Node(){}
    }
    
 //容器构造器
 public LRUCache(int capacity) {
        this.size=0;
        this.capacity=capacity;
        this.head=new Node();
        this.tail=new Node();
        head.next=tail;
        tail.prev=head;
        
    }
````

完全代码有几个helper方法：addToHead(每次新加都加到head)，RemoveNode(删除节点)，MoveToHead（把Node移动到head），removeTail（删除尾部），因为有伪节点，不需要判断null
 
```` 
//先建立node的两条线，再去弄别人的
    private void addToHead(Node node){
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;


    }
    
    private void removeNode(Node node){
        node.prev.next=node.next;
        node.next.prev=node.prev;
    }
    
    private void moveToHead(Node node){
        removeNode(node);
        addToHead(node);
    }
    
    private Node removeTail(){
        Node res=tail.prev;
        removeNode(res);
        return res;
    }
    
````

完整代码： get/replace就是遍历
 
```` 
class LRUCache {
    private int size;
    private int capacity;
    private Node head;
    private Node tail;
    
    //private HashMap<Integer,Node> cache=new HashMap<>();

    public LRUCache(int capacity) {
        this.size=0;
        this.capacity=capacity;
        this.head=new Node();
        this.tail=new Node();
        head.next=tail;
        tail.prev=head;
        
    }
    
    public int get(int key) {
        if(size==0){
            return -1;
        }
        Node temp=head;
        while(temp!=tail){
            if(temp.key==key){
                moveToHead(temp);
                return temp.val;
            }
            temp=temp.next;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(get(key)!=-1){
            replace(key,value);
            return;
        }
        //add key
        Node newNode=new Node(key,value,null,null);
        addToHead(newNode);
        size++;
        if(size>capacity){
            removeTail();
            size--;
        }
    }
    
    private void replace(int key,int value){
        Node temp=head;
        while(temp!=tail){
            if(temp.key==key){
                moveToHead(temp);
                temp.val=value;
                
            }
            temp=temp.next;
        }
    }
    
    //先建立node的两条线，再去弄别人的
    private void addToHead(Node node){
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;


    }
    
    private void removeNode(Node node){
        node.prev.next=node.next;
        node.next.prev=node.prev;
    }
    
    private void moveToHead(Node node){
        removeNode(node);
        addToHead(node);
    }
    
    private Node removeTail(){
        Node res=tail.prev;
        removeNode(res);
        return res;
    }
    
    private class Node{
        int key;
        int val;
        Node next;
        Node prev;
        
        public Node(int _key,int _val,Node _next,Node _prev){
            this.key=_key;
            this.val=_val;
            this.next=_next;
            this.prev=_prev;
        }
        
        public Node(){}
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
````





