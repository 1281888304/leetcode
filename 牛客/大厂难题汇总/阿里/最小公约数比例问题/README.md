<img width="970" alt="Screen Shot 2022-07-26 at 8 30 32 PM" src="https://user-images.githubusercontent.com/59748598/181154604-1a21bba7-8f41-47eb-8114-6e622f58725a.png">

这道题其实可以看成最小公约数，比如1000 500的公约数是1，就是1000 500找出两个unit最小单位，这里最小单位是Math.min(A/a,B/b)

1000 500 对应最小的是333，然后unit X a / unit X b就是答案

最下公约数算法：
<img width="684" alt="Screen Shot 2022-07-26 at 8 32 54 PM" src="https://user-images.githubusercontent.com/59748598/181154870-f9f18235-25b6-4c1f-92ef-ef79729fc71d.png">

GCD就是找最小公约数，直到把一个变成0

这里顺便科普下最大公倍数

m n 的最大公倍数是 (m X n)/最小公约数

Leetcode粘贴
```` 
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] params = br.readLine().trim().split(" ");
        int A = Integer.parseInt(params[0]), B = Integer.parseInt(params[1]), a = Integer.parseInt(params[2]), b = Integer.parseInt(params[3]);
        int greatestCommonDivisor = gcd(a, b);
        // 先约分
        a /= greatestCommonDivisor;
        b /= greatestCommonDivisor;
        // 然后计算unit
        int unit = Math.min(A / a, B / b);
        // x占a份unit，y占b份unit
        System.out.println(unit * a + " " + unit * b);
    }
    
    private static int gcd(int a, int b){
        if(a < b){
            int temp = a;
            a = b;
            b = temp;
        }
        while(b > 0){
            int temp = a % b;
            a = b;
            b = temp;
        }
        return a;
    }
}
````




