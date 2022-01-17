<img width="795" alt="Screen Shot 2022-01-14 at 9 42 08 PM" src="https://user-images.githubusercontent.com/59748598/149610567-f5e4e2ee-edce-4299-8a82-1180a54cb929.png">

关键是最上面放一个出口，即结束的
撤销操作是因为尝试失败了，撤销掉，尝试另外的可能

经典的不需要for loop leetcode 93，784答案需要从头撸到尾，这种不可能用forloop

但是不是每次都要撤销，看情况而定，大部分需要，比如说在小岛改变130，这里我们需要改变里面的东西，就不用，撤销大部分是用在不需要改变给定参数的

经常有要把小list加到大的list（result）里面，为什么要用add new ArrayList呢，因为如果不这样做，就是把地址加了进去，加进去以后回溯会继续对这个小的list惊醒操作，那么result这里的list就会变（因为是加的是地址）

visited数组（boolean） 和start/index都是一个避免一个数字重复使用的问题,

但是index/start有多一种情况，因为开始的时候for(int i=start/index)可以避免从后往前加 比如了leetcode78，用了boolean就会出现[3,2,1]这种答案不要的

有的时候我们为什么for loop里i>start/index才判断和前面数字一样吗，因为我们不想反复的加，通过回溯的时候index是和i一样的可以加，不让顺着for loop时候加（leetcode 90）

这里的i>index保证了如果i=index，然后两个一样是可以加的（回溯的时候可以加），但是从for loop顺上去不可以加，就避免了for loop循环上去的重复，
一般是递归过去一种，for loop一种，有duplicate就可以这样避免

剪枝就是有的枝跳过，经典题目leetcode 60
https://leetcode-cn.com/problems/permutation-sequence/solution/hui-su-jian-zhi-python-dai-ma-java-dai-ma-by-liwei/



