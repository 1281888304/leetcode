https://leetcode-cn.com/problems/continuous-subarray-sum/solution/de-liao-wo-ba-qian-zhui-he-miao-de-gan-g-c8kp/

经典的在一个数组里面找和为target的subarray个数或者有没有，不是all possible所以不用回溯，经典套路是用HashMap，key一般存sum或者整除；如果是找not least leetcode 209用inner loop


前缀不管是map还是array，第一个都是0；
map.put(0,1);    or    sum[n+1]; start loop from i=1
因为这里存的是次数才要放1，索引index的话是-1；
放了1，比如说题目560[4,5,0,0] k=4第一次loop才会有结果

有的情况下map先put，就不用放1，但大部分套路都是后放。整➗的题目类型，
[4,5] k=5在这种情况下，每次放进去，res都会加，因为不是放sum



[5,0,0,0]
3
https://leetcode-cn.com/problems/continuous-subarray-sum/solution/de-liao-wo-ba-qian-zhui-he-miao-de-gan-g-c8kp/


为什么preSum 的res是+=，因为比如说题目560 [4,5,0,0] k=5
在i=3 loop到0的时候，此时map(4,3)这里的原来的res+=3  => res=res+3
加上之前的res，为什么3是因为本来[4,5,0]的话，5多了一个，0也多了一个，还多了一个他自己（也不一定非是0，也有可能是负数）

题目974



int key = (presum % K + K) % K;

[-1,2] k=2这里的话，直接sum%k就没有了，因为在loop到2时候，key==1，但是之前没存，存的是-1

如果是abs绝对值的话[2,-2,2,-4] k=6
最后key==-2 =>2又把之前的加多了，实际上如果是最后一个是正4才有的效果
因为presum去的是余数永远<=k，-2在这里+6==4=>key =4,下面再来一个2就够了多一个2碰到sum==0再把前面的每个都加多一个（[2,-2,2,-4,2]）这种情况下是res=4





