https://github.com/azl397985856/leetcode/blob/master/thinkings/union-find.md

https://blog.csdn.net/yuzhiqiang666/article/details/80721436

原理链接，就是把不同的连在一起，下面那个链接是基于size和rank的优化

可以选择用map（key current节点，value 父亲节点）或者array，leetcode 947这种判断一共有多少个连通集合，用map更好，因为每次查找可以通过contains判断是否有，每次出现一次+1，
而且map是每一次连接的时候判断是否出现过（containsKey），map的size才会+1，array是一开始就设定好root的父节点是自己，只能通过判断父亲节点是否为自己来判断是否出现过，
但是如果这个root刚好是之前出现过但是也是其中一个连通集合的root（即父亲节点还是本身），就没办法判断出现了几次。还要通过添加visited HashSet判断，很浪费速度。

721合并邮件
