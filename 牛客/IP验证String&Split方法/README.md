
<img width="728" alt="Screen Shot 2022-06-16 at 6 10 54 PM" src="https://user-images.githubusercontent.com/59748598/174202605-5d8938ff-fc74-4d57-b77c-eaa3c630373d.png">

很简单就是判断是ipv4/ipv6

注意几个点122.222.111.1 这样的split(.) 出不来，要split("\\.")才可以

然后还有一个split("XXX",-1)

2.1 分割字符串时，使用limit = -1的split函数，使得字符串末尾或开头有一个'.'或':'也能分割出空的字符串

用try catch避免不是数字

```` 
import java.util.*;


public class Solution {
    /**
     * 验证IP地址
     * @param IP string字符串 一个IP地址字符串
     * @return string字符串
     */
    public String solve (String IP) {
        // write code here
        //两个都查一遍
        return validIPv4(IP) ? "IPv4" : (validIPv6(IP)? "IPv6" : "Neither");
        
    }
    
    private boolean validIPv4(String IP){
        
        String[] arr=IP.split("\\.");
        System.out.print(arr[0]);
        if(arr.length!=4)
            return false;
        
        for(String num : arr){
            if(num.startsWith("0")){
                return false;
            }
            try{
                int n=Integer.parseInt(num);
                if(n<=0 || n>=256){
                    return false;
                }
            }catch(NumberFormatException numberFormatException){
                return false;
            }
        }
        
        return true;
    }
    
    private boolean validIPv6(String IP) {
    String[] strs = IP.split(":",-1);
    if (strs.length != 8) {
        return false;
    }
 
    for (String str : strs) {
        if (str.length() > 4 || str.length() == 0) {
            return false;
        }
        try {
            int val = Integer.parseInt(str, 16);
        } catch (NumberFormatException numberFormatException) {
            return false;
        }
    }
    return true;
}
    
    
}
````


