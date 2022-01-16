https://leetcode-cn.com/problems/permutation-sequence/solution/hui-su-jian-zhi-python-dai-ma-java-dai-ma-by-liwei/578279/

这里有动画解释怎么剪枝，然后一遍过，不需要往回撤销操作一步得到答案

精髓就是在于计算每一步的阶乘，看要怎么选，比如说n=4 k=9（也是动画里的，复习要结合动画一起）

第一层算出来1那里一共有3！个，六个答案，9>6 => k变成3 （9-6），为什么是3，4-1，（n-1） ，把自己排除掉 剪枝操作

去2那里，2也一样3！ 6个答案，现在k剩下3，肯定在2这里，所以往下走，path.append(2)

然后往下走了碰到选1，就只有(n-1-index)这个index是告诉第几层，比如刚才选了2，那么index就是1，，选了2 3，index就是2

n-1-index得到2 2！个选择(k)3>2 => k=3-2=1 剪枝操作

再往下走，还是按照顺序来1跳过了，2visited过了，到3，可以了k=1， 选择一共是1！（n-1-1） 2! k<2,path.addpend(3)

接下来以此类推得到（2，3，1，4），尽量配合动画

```` 
class Solution {
    public String getPermutation(int n, int k) {
         
        boolean[] visited=new boolean[n+1];
        int[] factorial=new int[n+1];
        calculator(factorial);
        StringBuilder path=new StringBuilder();
        bt(n,k,factorial,visited,0,path);
        return path.toString();
    }
    //这里的index代表了path的位数
    //index 在这一步之前已经选择了几个数字，其值恰好等于这一步需要确定的下标位置
    private void bt(int n,int k,int[] factorial,boolean[] visited,
                   int index,StringBuilder path){
        if(index==n){
            return;
        }
        //这里是计算如果未知的话，在这个index有多少种可能
        //到时候用k减去count，就可以跳过了
        int count=factorial[n-1-index];
        //从1开始，答案不可以有0
        for(int i=1;i<=n;i++){
            //如果计算过，就走
            if(visited[i]) continue;
            
            if(k>count){
                k-=count;
                continue;
            }
            
            path.append(i);
            visited[i]=true;
            bt(n,k,factorial,visited,index+1,path);
            // 注意 1：不可以回溯（重置变量），算法设计是「一下子来到叶子结点」，没有回头的过程
                    //因为这个设计的是，直接一步到位
            // 注意 2：这里要加 return，后面的数没有必要遍历去尝试了
            return;
        }
        
        
    }
    //阶乘， n！ 5！=1x2x3x4x5
    private void calculator(int[] factorial){
        factorial[0]=1;
        for(int i=1;i<factorial.length;i++){
            factorial[i]=factorial[i-1]*i;
        }
    }
}
````







