https://leetcode-cn.com/problems/qn8gGX/

<img width="557" alt="Screen Shot 2022-04-18 at 12 38 34 PM" src="https://user-images.githubusercontent.com/59748598/163866234-c5634fc8-600a-47c5-a324-9f33865720ae.png">


这里存的是两个arr的和，并且一个数字可以多次利用，比如说下面这个情况nums[0]就可能被二次应用

首先，利用两个数组都是升序的条件，结果中最小的组合肯定是 nums1[0] + nums2[0]。

但是，次小的是什么呢？ 是 nums1[0] + nums2[1] 还是 nums1[1] + nums2[0] 呢？我们不知道。

用最小堆存着索引，然后比每一个的和
```` 
// 优先级队列，保存 [index1, index2]
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> nums1[a[0]] + nums2[a[1]] - (nums1[b[0]] + nums2[b[1]]));



````

然后先add k次，把nums1的前k个和nums2[0]放到priorityQueue（这里放的是索引）（答案最多k个）

```` 
// 把 nums1 的所有索引入队，nums2 的索引初始时都是 0
        // 优化：最多入队 k 个就可以了，因为提示中 k 的范围较小，这样可以提高效率
        for (int i = 0; i < Math.min(k, nums1.length); i++) {
            heap.offer(new int[] {i, 0});
        }

````

然后while loop先把第一个拿出来，第一个拿出来以后第二小就是nums1[1] +nums2[0],然后我们把nums1[0]+nums2[1]放进去，对比下第二大是这两个哪个产生的，

以此类推，我们以后吧nums1[i]+nums[j]的索引i j从priorityQueue拿出来的时候，就把i，j+1加到堆里面，刚好就是下一个可以加的，然后让堆判断谁是最小的
```` 
class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        // 优先级队列，保存 [index1, index2]
        PriorityQueue<int[]> heap = 
        new PriorityQueue<>((a, b) -> nums1[a[0]] + nums2[a[1]] - (nums1[b[0]] + nums2[b[1]]));

        // 把 nums1 的所有索引入队，nums2 的索引初始时都是 0
        // 优化：最多入队 k 个就可以了，因为提示中 k 的范围较小，这样可以提高效率
        for (int i = 0; i < Math.min(k, nums1.length); i++) {
            heap.offer(new int[] {i, 0});
        }

        List<List<Integer>> res = new ArrayList<>();

        while(k>0 && !heap.isEmpty()){
            int[] position=heap.poll();
            int index1=position[0];
            int index2=position[1];
            res.add(Arrays.asList(nums1[index1],nums2[index2]));
            if((position[1]+1)<nums2.length){
                //heap.offer(new int[]{index1,index2});
                position[1]++;
                heap.offer(position);

            }
            k--;
        }
        return res;
    }
}

````



