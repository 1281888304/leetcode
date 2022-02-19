https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/

<img width="536" alt="Screen Shot 2022-02-19 at 3 22 29 PM" src="https://user-images.githubusercontent.com/59748598/154822364-4b68053c-15aa-4cc4-a6f7-89d162f6e9f0.png">


这道题就是找规律，step 1先找到那个区间，step 2找到对应哪一个数字，step 3在找对应这个数字中的哪一个（转成String用s.charAt()-'0'）

![image](https://user-images.githubusercontent.com/59748598/154822438-b02ccfca-df86-4d12-abb6-ed20557c72c2.png)

可以根据这样设置找到区间

![image](https://user-images.githubusercontent.com/59748598/154822447-7592dd8d-b13b-455d-b6d6-5ecfda2aaaa0.png)

然后根据剩下的n找到num（对应哪一个数字），剩下的n是因为不停的减变少

根据剩下的n找到第几位

 
```` 
class Solution {
    public int findNthDigit(int n) {
        if(n<=9) return n;

        int digit=1;
        long start=1;
        long count=9*start*1;
        //step 1
        while(n>count){
            n-=count;
            digit++;
            start*=10;
            count=9*start*digit;
        }

        //step2
        long num=start+(n-1)/digit;

        //step3
        int index=(int)(n-1)%digit;
        String s=String.valueOf(num);
        return s.charAt(index)-'0';
        //return Long.toString(num).charAt((n - 1) % digit) - '0';
    }
}
````







