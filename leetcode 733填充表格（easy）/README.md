<img width="626" alt="Screen Shot 2022-01-18 at 1 45 14 PM" src="https://user-images.githubusercontent.com/59748598/150023608-d836b038-f74b-45c6-bbcb-ea0cebf1b5fc.png">

题目是给定一个位子和颜色，让你把上下左右都变，相连的也是，类似于130和200题，就上下左右变，经典的不用撤销操作的

有一个坑，如果old color和new color一样直接return就完了，不然可能stack overflow，他一大半都是这个坑

```` 
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int color=image[sr][sc];
        //corner case
        if(color==newColor){
            return image;
        }
        bt(image,sr,sc,newColor,color);
        return image;
        
    }
    
    private void bt(int[][] image,int row,int col,int newColor,int oldColor){
        //两种出口，corner case在比较color前面
        if(row<0 || row>=image.length || col<0 || col >=image[0].length){
            return;
        }
        if(image[row][col]!=oldColor){
            return;
        }
        
        //更换color为new color
        image[row][col]=newColor;
        bt(image,row+1,col,newColor,oldColor);
        bt(image,row-1,col,newColor,oldColor);
        bt(image,row,col+1,newColor,oldColor);
        bt(image,row,col-1,newColor,oldColor);
        
    }
}
````




