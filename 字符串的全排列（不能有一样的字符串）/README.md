![image](https://user-images.githubusercontent.com/59748598/178372179-53f45b1c-7c66-4117-9ab6-34340952206f.png)

不停的用swap方法去交换头部，swap(arr,i,index)，当一开始i==index的时候，可以吧原本的加进来，顺着for loop往下走才会出现别的

import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param str string字符串 
     * @return string字符串ArrayList
     */
    public ArrayList<String> Permutation (String str) {
        // write code here
        ArrayList<String> res=new ArrayList<>();
        bt(str.toCharArray(),0,res);
        return res;
        
    }
    
    private void bt(char[] arr,int index,ArrayList<String> res){
        if(index==arr.length-1){
            String temp=new String(String.valueOf(arr));
            
            if(!res.contains(temp)){
                res.add(temp);
            return;
            }
        }
        for(int i=index;i<arr.length;i++){
            swap(arr,i,index);
            bt(arr,index+1,res);
            swap(arr,index,i);
        }
    }
    
    
    private void swap(char[] arr,int i,int j){
        if(i!=j){
            char temp=arr[i];
            arr[i]=arr[j];
            arr[j]=temp;
        }
    }
}
