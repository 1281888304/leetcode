https://leetcode-cn.com/problems/qiu-12n-lcof/submissions/

<img width="537" alt="Screen Shot 2022-03-17 at 11 31 27 AM" src="https://user-images.githubusercontent.com/59748598/158871813-03c547cd-615e-496e-af63-a7458db1daf7.png">

1+2+3=6不用for/while/if等，只能用递归了

很基础的递归，如果n==0 return 0

不然就一直加下去直到0

```` 
class Solution {
    public int sumNums(int n) {
        if(n==0){
            return 0;
        }
        return n+sumNums(n-1);
    }
}
````


