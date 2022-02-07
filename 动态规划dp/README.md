https://leetcode-cn.com/circle/article/2Xxlw3/

- Dynamic Programming ★★★★★★ for Google, ★ for Facebook
    - 绕不过的一道坎，但在这里实在是说不完，重点还是理解阶段状态转移三个概念(stage, state, transfer)，比如  f[i] = max{f[j]} + 1 (a[j] < a[i] ,j < i) 是LIS的转移方程，这里i 是阶段，f[i]是状态，后面的方程是转移，转移是有条件的，理清楚转移条件即可。 另外LIS的nlogn优化也建议掌握，我的Google第一轮就考到了，题目是披着LIS的外壳，仔细想想不难分析出来。
    - 掌握：背包（01、多重等简单背包掌握即可）、一维区间dp、树形dp、二维区间dp、记忆化搜索(dfs+memo)、LIS（nlogn）


1 背包问题，经典的是416，判断什么时候用dp二维数组。也可以看成硬币问题，如果一个硬币只能投一次，就二维数组。然后同理，有的是组合字符串，每个character只能用一次，也是背包问题dp二维数组
