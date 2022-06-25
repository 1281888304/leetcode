<img width="706" alt="Screen Shot 2022-06-24 at 8 41 21 PM" src="https://user-images.githubusercontent.com/59748598/175756862-8f211d90-f15d-49a5-b901-ec6985f44177.png">

<img width="505" alt="Screen Shot 2022-06-24 at 8 41 33 PM" src="https://user-images.githubusercontent.com/59748598/175756868-ba1be4fb-a751-4387-85bf-4fe3108487b7.png">

有一个需要注意的是，前导0怎么去除，我之前用了大量的if+while处理十分麻烦

String="0010003" 用IntegerparseInt之后就会变成10003自动去除掉前面的0，很方便

代码：
```` 
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 比较版本号
     * @param version1 string字符串 
     * @param version2 string字符串 
     * @return int整型
     */
    public int compare (String version1, String version2) {
        // write code here
        String[] arr1=version1.split("\\.");
        String[] arr2=version2.split("\\.");
        int index1=0,index2=0;
        while(index1<arr1.length || index2<arr2.length){
            int n1=index1>=arr1.length ? 0 : Integer.parseInt(arr1[index1]);
            int n2=index2>=arr2.length ? 0 : Integer.parseInt(arr2[index2]);
            if(n1>n2){
                return 1;
            }
            else if(n1<n2){
                return -1;
            }
            index1++;
            index2++;
        }
        return 0;
    }
}
````






