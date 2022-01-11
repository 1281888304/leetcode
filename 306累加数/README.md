这里的解法就很暴力很dfs，第一个for loop用i来确定第一个数first，第二个inner loop用j来确定第二个数second，第一个for loop确定好第一个，第二个inner for loop就尝试着把所有的第一个的可能都尝试一遍

然后把first和second放到dfs里，如果找到了third就把second替换成first，third替换成second继续dfs

我犯了一个小问题，之前void习惯了直接dfs就继续往下走，boolean和其他有返回值的，要合适的方法去调动这个函数

直接dfs往下走能跑是能跑，但是有问题，而且逻辑大多也不对，设计成boolean就是有返回的

三个corner case：first开始为0 因为原理是用找substring(0,i+1)，不断尝试着组合，如果组合成功就返回true， 但是这里有一个问题，如果第一个是0，下一个for loop组合失败意味着全部尝试完了，接下来如果成功的话，
就是比如说0235这样也可以，但是就违背了

second开始为0 如果第二个开始是0，就break，尝试用第一个for loop改变first， 不能直接和上一个for loop一样return false比如10 2 102，first是1 和 second是0不可以返回false，要改变first再试一下

third开始为0就和第一个一样了，因为他开始为0他只能是0，直接在遍历到后一位return false，因为如果 0000000的话，遍历到前一位会继续往下走，就成功了，遍历到后一位肯定就是不成功的，1203这种情况如果
不return false，答案就错了

class Solution {

    public boolean isAdditiveNumber(String num) {
        int n=num.length();
        char[] nums=num.toCharArray();
        //因为最少后面要留两个
        //i代表第一个数，j代表第二个数
        for(int i=0;i<n-2;i++){
            //corner case
            //因为原理是用找substring(0,i+1)，不断尝试着组合，如果组合成功就返回true
            //但是这里有一个问题，如果第一个是0，下一个for loop组合失败，接下来如果成功的话
            //就是比如说0235这样也可以，但是就违背了
            if(nums[0]=='0' && i>0){
                return false;
            }
            //用j来得到第二个数
            //最少要留多一个数
            for(int j=i+1;j<n-1;j++){
                //第二个corner case，如果第二个开始是0，就break，尝试变first
                //不能return false比如10 2 102
                //first 1 和 second 0不可以返回false
                if(nums[i+1]=='0' && j > i+1){
                    break;
                }
                
                //0到i
                Long first=Long.parseLong(num.substring(0,i+1));
                //i+1到j
                Long second=Long.parseLong(num.substring(i+1,j+1));
                if(dfs(first,second,num,j+1)){
                    return true;
                }
            }
        }
        return false;
    }
    //index代表second最后一位的后一位，third的开始index，thirdIndex
    private boolean dfs(Long first,Long second,String num, int index){
        //出口，走到最后了，
        if(index==num.length()){
            return true;
        }
        //用for loop遍历不同的i，找到如果有满足的，第二个变成第一个，第三个变成第二个
        //开始经典的回溯算法
        for(int i=index;i<num.length();i++){
            Long third=Long.parseLong(num.substring(index,i+1));
            // 同样第三个数字只能为0，在第三个数字为0的情况下还没找到正确结果的情况下直接返回false即可
            //举个例子1203这个情况，如果不返回false就返回true了，所以遍历到3这里的时候必须要返回false
            if(num.charAt(index)=='0' && i>index){
                return false;
            }
            if(third>first+second){
                return false;
            }else if(third==first+second){
                if(dfs(second,third,num,i+1)){
                    return true;
                }
            }
        }
        return false;
    }
}

