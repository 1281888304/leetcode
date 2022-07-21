<img width="717" alt="Screen Shot 2022-07-20 at 6 02 57 PM" src="https://user-images.githubusercontent.com/59748598/180107707-fdf366f7-8735-4d29-acdb-d4ca5dd31497.png">

这样从左往右，上往下都是递增，可以从左下角开始，如果target>current 往上走一步，如果target<cur 往右一步直到到右上角为止

也可以右下角到左上角，一样的

Leetcode粘贴
```` 
public class Solution {
    public boolean Find(int target, int [][] array) {
        //从后往前
        int m=array.length;
        int n=array[0].length;
        if(array==null || m==0 || n==0){
            return false;
        }
        int row=m-1,col=0;
        while(true){
            if(row<0 || col>=n){
                break;
            }
            int cur=array[row][col];
            if(target==cur){
                return true;
            }
            else if(target>cur){
                col=col+1;
            }
            else{
                row=row-1;
            }
        }
        
        return false;
    }
}
````


