https://leetcode-cn.com/problems/nZZqjQ/


<img width="543" alt="Screen Shot 2022-03-11 at 7 25 20 PM" src="https://user-images.githubusercontent.com/59748598/158001931-613d77e7-9aaf-44bb-b19a-271e1b7b2d85.png">

用binary search做，有一个关键是，这里怎么找到和mid对比的target

target其实是mid作为这一次猩猩吃香蕉的食量，判断吃完一共需要多少个小时

left=1 right等于最大值，用方法吧need hour算出来，我之前用taotal/h，是错误的

```` 
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        //int left=1;
        Arrays.sort(piles);

        int right=piles[piles.length-1];
        int left=1;
        while(left<right){
            int mid=left+(right-left)/2;
            
            
            if(needHour(piles,mid)>h) left=mid+1;
            else right=mid;
        }
        return left;
    }


    private int needHour(int[] piles, int eat) {
        int total = 0;
        for (int pile : piles) {
            int hour = pile / eat;
            // 若  hour * eat == pile，表示 pile 可以被 eat 整除
            total += hour * eat == pile ? hour : hour + 1;
        }
        return total;
    }


}
````




