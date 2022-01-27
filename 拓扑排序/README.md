207题的题解动画做得很好，就是一个个去掉 

https://leetcode-cn.com/problems/course-schedule/solution/course-schedule-tuo-bu-pai-xu-bfsdfsliang-chong-fa/

拓扑排序一般会有一个rank/degree，然后有一个queue。queue在一开始会吧rank/degree=1的点加进去，即只能影响一个的点，然后把被他影响的拿出来再放进queue，因为满足后放先拿，所以如果1影响2，2影响3，4，不管queue里有多少个类似于1这样只能影响一个的点顺序都是1 2 3 4来处理，把和1处理完了才去处理下一个rank/degree==1的点




