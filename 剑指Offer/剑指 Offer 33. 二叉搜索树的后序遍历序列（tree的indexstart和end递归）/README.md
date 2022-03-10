https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/

<img width="562" alt="Screen Shot 2022-03-09 at 5 59 10 PM" src="https://user-images.githubusercontent.com/59748598/157573286-b3d15c1d-8c79-4a97-adf6-88654b600d85.png">


利用了postorder left->right->root 可以确认最后一个是root，分割开成为小的也是root在最后面

然后利用root分开左边和右边，分开的方式：左边全部比root小，右边全部比root大，通过找到第一个比root大的就是右边第一个，然后确认这个，不停的递归就好了，利用start end来分割数组

![image](https://user-images.githubusercontent.com/59748598/157573458-d8cdc16f-a2a5-44bb-bdd4-88440f75a221.png)


代码先找到firstRight（），然后在用判断是不是root比左边全部都大，比右边全部都笑

实现方式：找到第一个比root大的，然后看是不是从这个开始全部比root大

```` 
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return check(postorder,0,postorder.length-1);
    }

    public boolean check(int[] postorder,int start,int end){
        //说明到了最下面
        if(start>=end) return true;
        int rootVal=postorder[end];
        int right=start;
        while(postorder[right]<rootVal){
            right++;
        }
        int firstRight=right;
        while(postorder[right]>rootVal){
            right++;
        }
        return (right==end) && check(postorder,start,firstRight-1)
            && check(postorder,firstRight,end-1);

    }

    
}





//递归或者怎样让array size只有2的时候，保证递增就好
````




