https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/


<img width="562" alt="Screen Shot 2022-03-15 at 10 28 39 AM" src="https://user-images.githubusercontent.com/59748598/158436487-3bbf7e85-f55b-4f36-b7fd-98a87858ee6e.png">

这里要考虑大数字，不能直接for loop，用全排列按顺序一个个排序

全排列两位和第一位是1：10 11 12 13 .........19

所以我们要考虑两个问题，有多少位（digit）和第一个数字first，用inner for loop去loop char来解决，注意，char也是可以和int一样加减的

```` 
for(int digit=1;digit<=n;digit++){
            //set first
            for(char first='1';first<='9';first++){
                char[] nums=new char[digit];
                nums[0]=first;
                //从index=1第二位开始
                dfs(nums,1);
            }
        }
````

传统的是list.add，用数组的话就不用，用int数组 和count,在这道题因为n=1是1到9，数组大小记得-1
```` 
int[] res=;
int count=0;
res[count++]=;
````
怎么按顺序排列

这里因为不是list是数组，没有撤销操作

保证顺序100 101 102； 当index一直等于2的时候，顺着for loop一路就不停的替换掉最后一个，跑完这个for loop return回去前一个，从110继续开始
```` 
for(char i='0';i<='9';i++){
            nums[index]=i;
            dfs(nums,index+1);
        }
````

完整代码：
```` 
class Solution {
    int[] res;
    int count=0;
    public int[] printNumbers(int n) {
        //1 to 9 skip first 0
        int len=(int) Math.pow(10,n)-1; 
        res=new int[len];
        for(int digit=1;digit<=n;digit++){
            //set first
            for(char first='1';first<='9';first++){
                char[] nums=new char[digit];
                nums[0]=first;
                //从index=1第二位开始
                dfs(nums,1);
            }
        }

    }

    public void dfs(char[] nums,int index){
        if(index==nums.length-1){
            res[count++]=Integer.parseInt(String.valueOf(nums));
            return;
        }
        //这里因为不是list是数组，没有撤销操作
        //保证顺序100 101 102； 当index一直等于2的时候，顺着for loop一路就不停的替换掉最后一个，跑完这个for loop
        // return回去前一个，从110继续开始
        for(char i='0';i<='9';i++){
            nums[index]=i;
            dfs(nums,index+1);
        }
    }
}
````







