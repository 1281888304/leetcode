<img width="541" alt="Screen Shot 2022-02-15 at 4 26 19 PM" src="https://user-images.githubusercontent.com/59748598/154172847-0fd1b6a6-2d52-4e19-b187-ca634a20c5dc.png">

从后往前找，每一行最小的都是第一个，如果target小于第一个就看上一行，然后如果target大于第一行就往右走尝试着去找，如果走到最右边还没有就再看上一行，如果第一行都走完了就返回false

重点就是从后找，然后跳过不用的行

```` 
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        int row=matrix.length-1,col=0;

        while(row>=0 && col<matrix[0].length){
            if(target<matrix[row][col]){
                row--;
            }
            else if(target>matrix[row][col]){
                col++;
            }
            else{
                return true;
            }
        }
        return false;
    }
}
````




