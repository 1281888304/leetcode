左边如果是空不用考虑，下一次递归end<=start自动返回true，右边如果为空，firstLarge需要考虑
```` 
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        if(postorder==null || postorder.length<1) return true;
        int n=postorder.length;
        return check(postorder,0,n-1);
    }

    public boolean check(int[] arr,int start,int end){
        if(end<=start) return true;
        
        int root=arr[end];
        int firstLarge=-1;
        for(int i=start;i<=end-1;i++){
            if(arr[i]>root){
                firstLarge=i;
                break;
            }
        }
        
        if(firstLarge!=-1){
            for(int i=firstLarge;i<=end-1;i++){
                if(arr[i]<root){
                    return false;
                }
            }
            boolean right=check(arr,firstLarge,end-1);
            boolean left=check(arr,start,firstLarge-1);
            return (left && right);
        }
        else{
            boolean left=check(arr,start,end-1);
            boolean right=true;
            return (left && right);
        }
        
        

    }
}
// root是最后一个

````


