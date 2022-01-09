计算质数，从2开始算，任何一个只能被自己整除的数算质数
我第一次以为只有2 3 57作为basic prime number
其实还有很多比如说11 13，所以说，这道题就是用boolean的数组
从2开始往上乘，所有能乘到的都不算质数，记得要做一个小插曲，比如说8的话，2那边的倍数已经解决了，就没必要再来一次了

class Solution {

    public int countPrimes(int n) {
        if(n<=2) return 0;
        
        boolean[] isPrime=new boolean[n+1];
        Arrays.fill(isPrime,true);
        //把所有非质数变成false
        for(int i=2;i*i<n;i++){//所有i的倍数都变成false
            //这一步是为了避免浪费时间，比如说8的话，2那边肯定搞完了
            //2 3 5 7不够，11 13的倍数也要考虑，一开始的失误
            if(isPrime[i]){
                for(int j=i*i;j<n;j+=i){
                    isPrime[j]=false;
                }
            }
        }
        //计算所有的true（质数）
        int res=0;
        for(int i=2;i<n;i++){
            if(isPrime[i]){
                res++;
            }
        }
        return res;
    }
}
