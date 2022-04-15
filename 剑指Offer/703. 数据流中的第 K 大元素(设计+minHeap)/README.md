https://leetcode-cn.com/problems/jBjn9C/

<img width="508" alt="Screen Shot 2022-04-14 at 11 50 44 PM" src="https://user-images.githubusercontent.com/59748598/163533001-235202de-95c7-4c11-880c-7fb8198a3663.png">


其实很简单，既然他要第K大，那就用PriorityQueue实现一个最小堆minHeap，保证minHeap里只有k个数（都是最大的那几个），然后peek（最小）的就是答案

比如说[2,3,4,5,6,7,8] k=4，那就让heap只有[5,6,7,8]，5是peek也就是答案

加一个10就把5去掉变成[6,7,8,10]6是peek也是答案

在加一个2，把2去掉还是6，7，8，10]

代码：
```` 
class KthLargest {
    private PriorityQueue<Integer> minHeap;
    private int k;

    public KthLargest(int k, int[] nums) {
        this.k=k;
        minHeap=new PriorityQueue<>((a,b)->a-b);
        for(int i=0;i<nums.length;i++){
            minHeap.add(nums[i]);
            
        }
    }
    
    public int add(int val) {
        minHeap.add(val);
        while(minHeap.size()>k){
            minHeap.poll();
        }
        return minHeap.peek();
    }
}
````




