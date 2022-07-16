https://www.nowcoder.com/practice/389fc1c3d3be4479a154f63f495abff8?tpId=295&tqId=1375231&ru=/exam/oj&qru=/ta/format-top101/question-ranking&sourceUrl=%2Fexam%2Foj

这里分析的很好，简单而言用了位运算逻辑

 & 与运算 两个位都是 1 时，结果才为 1，否则为 0 0001 & 0011= 0001 
 
| 或运算 两个位都是 0 时，结果才为 0，否则为 1 0001 ｜0011=0011

^ 异或运算，两个位相同则为 0，不同则为 1  0001 ^ 0011 =0010

算法中如果是找到一个的话，便利数组全部异或^一次就好了，毕竟出现两次或者偶数次可以通过异或消掉 

0011 ^0011=0000 

0011^0011 ^anyNumber =anyNumber

<img width="699" alt="Screen Shot 2022-07-15 at 5 30 01 PM" src="https://user-images.githubusercontent.com/59748598/179327071-e008f9dd-d65f-4ca9-95d4-458f697c8127.png">



现在要两个，就要找到一个数字mask把这两个数字区分开来， n1& mask=0  n2 &mask!=0

其他的出现时偶数次，可以通过异或消除掉

![image](https://user-images.githubusercontent.com/59748598/179327674-9d0d819c-b04a-4e49-ae86-238653817337.png)

先全部异或比如 [1,1,3,6] 异或完 1^1^3^6 == 3^6 == 0101(5)记录为tmp

3(0011) 6(0110) 不同的是第一位和第三位，这个时候取最右边的就可以了记录位mask，这样在一个位置上一个有一个没有mask

注意：tmp的0101的两个1可能来源于不同的两个数字，所以我们找的mask必须只有一个1，那样就可以让n1 n2 & mask一个位0一个不是0，从最右边走

代码：
```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param array int整型一维数组 
     * @return int整型一维数组
     */
    public int[] FindNumsAppearOnce (int[] array) {

        // 先将全部数进行异或运算，得出最终结果
        int tmp = 0;
        for(int num: array){
            tmp ^= num;
        }

        // 找到那个可以充当分组去进行与运算的数,tmp可能不止一个1
        // 从最低位开始找起
        int mask = 1;
        while((tmp&mask) == 0){
            mask <<= 1;
        }

        // 进行分组，分成两组，转换为两组 求出现一次的数字 去求
        int a = 0;
        int b = 0;
        for(int num:array){
            //不管有多少个别的数，出现两次或者偶数次，都会被消掉
            if((num&mask) == 0){
                a ^= num;
            }else{
                b ^= num;
            }
        }
        // 因为题目要求小的数放前面，所以这一做个判断
        if(a > b){
            int c = a;
            a = b;
            b = c;
        }
        return new int[]{a,b};
    }
        
        
        
    
}
````





