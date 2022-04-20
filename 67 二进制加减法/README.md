https://leetcode-cn.com/problems/JFETK5/submissions/

<img width="562" alt="Screen Shot 2022-04-19 at 10 35 58 PM" src="https://user-images.githubusercontent.com/59748598/164157672-3ecea4df-7c7d-4d2d-88aa-85f29520fc8a.png">



![image](https://user-images.githubusercontent.com/59748598/164157657-055bf756-f0db-4ce7-a767-b90987b69d37.png)

无非就是三种可能 1+1 =10。
1+0=0
1+1+1（carry）=11

如果1+1 /1+1+1 =》carry =1要不然0

然后看sum是等于1/2/3三种可能，看是append 1还是0

```` 
int sum=numA+numB+carry;
            if(sum>=2){
                carry=1;
            }
            else{
                carry=0;
            }
            if(sum%2==0){
                sb.append(0);
            }else{
                sb.append(1);
            }
````
完整代码：这里while loop用的好，carry/a/b三个又一个不停下来loop就无法结束
```` 
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb=new StringBuilder();
        int i=a.length()-1,j=b.length()-1;
        int carry=0;
        //三个人和一个都不可以停下来
        while(i>=0 || j>=0 || carry>0){
            int numA=(i>=0) ? a.charAt(i)-'0' :0;
            int numB=(j>=0) ? b.charAt(j)-'0' :0;
            int sum=numA+numB+carry;
            if(sum>=2){
                carry=1;
            }
            else{
                carry=0;
            }
            if(sum%2==0){
                sb.append(0);
            }else{
                sb.append(1);
            }
            i--;
            j--;
        }
        return sb.reverse().toString();
    }
}
````




