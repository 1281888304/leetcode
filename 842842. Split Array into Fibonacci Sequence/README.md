<img width="811" alt="Screen Shot 2022-01-14 at 9 30 03 PM" src="https://user-images.githubusercontent.com/59748598/149610293-aaaf54d4-687d-4a8e-a8f9-2262672941a4.png">

就是经典的回溯，一个个往res里面加，如果可以的话就return true停下来，不然就false

为什么用boolean不用void：

为什么需要boolean，因为如果是boolean，那么回溯以后，可以停在撤销操作那一步，

不然的话，如果是void，撤销操作这一步就必须走，这样res永远是空的，因为会撤销，这一步是为了让有另外一个大的res来把这个小的吸收的套路

试过如果找一个也是List<Integer> last来吸收res，也可以，代码在下面，但是要考虑另外一个问题，就是如果答案有两个可能，比如给的"1101111"
    
有110 1 111 和11 0 11 11两个正确答案，这也是唯一过不了的，答案唯一的话就可以过

下面那个方法是用来得到一个long的数字，为什么是long，因为有可能得到数字比Integer.MAX_VALUE还要大的

class Solution {

    public List<Integer> splitIntoFibonacci(String num) {
        List<Integer> res=new ArrayList<>();
        char[] nums=num.toCharArray();
        bt(nums,res,0);
        return res;
    }
    
    
    private boolean bt(char[] nums, List<Integer> res,int index){
        if(index==nums.length && res.size()>=3){
            return true;
        }
        for(int i=index;i<nums.length;i++){
            //corner case,两位数不可以为0
            if(nums[index]=='0' && i>index){
                break;
            }
            long num=subDigit(nums,index,i);
            //如果截取的数字大于int的最大值，则终止截取
            if (num > Integer.MAX_VALUE) {
                break;
            }
            //暂时res的size
            int size=res.size();
            
            //如果size大于等于2的时候出现坏的情况
            //坏的情况：数字大于res最后两个
            if(size>=2 && num>res.get(size-1) +res.get(size-2)){
                return false;
            }
            
            //好的情况，res没有两个数，就要往里加
            //或者刚好等于了
            if(size<2 || num==res.get(size-1) + res.get(size-2)){
                //先加进去
                res.add((int)num);
                //尝试着往下一步走
                if(bt(nums,res,i+1)){
                    return true;
                }
                //如果没走成功，就撤销操作
                res.remove(res.size()-1);
            }
            
        }
        return false;
    }
    
    //相当于截取字符串S中的子串然后转换为十进制数字
    private long subDigit(char[] digit, int start, int end) {
        long res = 0;
        for (int i = start; i <= end; i++) {
            res = res * 10 + digit[i] - '0';
        }
        return res;
    }

}

class Solution {
    List<Integer> last=new ArrayList<>();
    public List<Integer> splitIntoFibonacci(String num) {
        List<Integer> res=new ArrayList<>();
        char[] nums=num.toCharArray();
        bt(nums,res,0);
        return last;
    }
    
    
    private void bt(char[] nums, List<Integer> res,int index){
        if(index==nums.length && res.size()>=3){
            for(int i=0;i<res.size();i++){
                last.add(res.get(i));
            }
            return;
        }
        for(int i=index;i<nums.length;i++){
            //corner case,两位数不可以为0
            if(nums[index]=='0' && i>index){
                break;
            }
            long num=subDigit(nums,index,i);
            //如果截取的数字大于int的最大值，则终止截取
            if (num > Integer.MAX_VALUE) {
                break;
            }
            //暂时res的size
            int size=res.size();
            
            //如果size大于等于2的时候出现坏的情况
            //坏的情况：数字大于res最后两个
            if(size>=2 && num>res.get(size-1) +res.get(size-2)){
                return;
            }
            
            //好的情况，res没有两个数，就要往里加
            //或者刚好等于了
            if(size<2 || num==res.get(size-1) + res.get(size-2)){
                //先加进去
                res.add((int)num);
                //尝试着往下一步走
                bt(nums,res,i+1);
                //如果没走成功，就撤销操作
                res.remove(res.size()-1);
            }
            
        }
        //return false;
    }
    
    //相当于截取字符串S中的子串然后转换为十进制数字
    private long subDigit(char[] digit, int start, int end) {
        long res = 0;
        for (int i = start; i <= end; i++) {
            res = res * 10 + digit[i] - '0';
        }
        return res;
    }

}

    



