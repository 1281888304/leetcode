https://leetcode-cn.com/problems/smallest-difference-lcci/

<img width="533" alt="Screen Shot 2022-03-19 at 11 56 22 AM" src="https://user-images.githubusercontent.com/59748598/159134749-cec26f91-f9ea-4a4a-8582-6e9fcabb1ceb.png">

先sort两个array ，然后指针都设为最左边一个个挪动，规律如下。如果A比B大，就把A往右挪，否则就B往右挪

```` 
class Solution {
    public int smallestDifference(int[] a, int[] b) {
        Arrays.sort(a);
        Arrays.sort(b);
        int i=0,j=0;
        long res= Long.MAX_VALUE;
        while(i<a.length && j<b.length){
            long A=(long)a[i];
            long B=(long)b[j];
            if(A==B){
                return 0;
            }
            else if(A>B){
                res=Math.min(A-B,res);
                j++;
            }
            else{
                res=Math.min(B-A,res);
                i++;
            }
        }
        return (int)res;
    }
}
````




