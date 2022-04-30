<img width="1193" alt="Screen Shot 2022-04-29 at 10 08 14 PM" src="https://user-images.githubusercontent.com/59748598/166092032-ff2b2256-4cd3-4747-bbeb-6540ad91b49b.png">

这道题有点独特，给定n行m列就是n x m;每次旋转不仅要n和m交换，还要考虑变换问题

进行一次顺时针旋转，原来第i行就变成倒数第i列，第j列就变成第j行，逆时针旋转相反；水平反转仅将原来第j列变成倒数第j列。直接坐标变换就行，但是我们注意到一个细节，逆时针或顺时针旋转4次相当于没转，水平反转2次相当于没转，因此可以通过取模进一步降低时间复杂度。

图片详解：
![image](https://user-images.githubusercontent.com/59748598/166092137-0b7b79af-2bd2-4540-93f9-5efd9f69ba3c.png)


顺时针旋转：
```` 
private static int[] clockwise(int[] pos, int times){
        times=times%4;
        
        while(times-->0){
            int new_j=n-pos[0]+1;
            pos[0]=pos[1];
            pos[1]=new_j;
            //nxm -> mxn
            int temp=n;
            n=m;
            m=temp;
        }
        
        return pos;
    }
````
其他同理，水平反转就是横坐标不变，纵坐标变
 
```` 
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {
    public static int n;
    public static int m;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] params = br.readLine().trim().split(" ");
        int x = Integer.parseInt(params[0]);
        int y = Integer.parseInt(params[1]);
        int z = Integer.parseInt(params[2]);
        params = br.readLine().trim().split(" ");
        int rows = Integer.parseInt(params[0]);
        int cols = Integer.parseInt(params[1]);
        int q = Integer.parseInt(br.readLine());
        for(int i = 0; i < q; i++){
            n = rows;
            m = cols;
            params = br.readLine().trim().split(" ");
            int x1 = Integer.parseInt(params[0]);
            int x2 = Integer.parseInt(params[1]);
            int[] pos = new int[]{x1, x2};
            pos = antiClockwise(flip(clockwise(pos, x), y), z);
            System.out.println(pos[0] + " " + pos[1]);
        }
    }
    //进行一次顺时针旋转，原来第i行就变成倒数第i列，第j列就变成第j行，逆时针旋转相反；
    //水平反转仅将原来第j列变成倒数第j列。直接坐标变换就行，但是我们注意到一个细节，逆时针或顺时针旋转4次相当于没转，水平反转2次相当于没转，因此可以通过取模进一步降低时间复杂度
    private static int[] clockwise(int[] pos, int times){
        times=times%4;
        
        while(times-->0){
            int new_j=n-pos[0]+1;
            pos[0]=pos[1];
            pos[1]=new_j;
            //nxm -> mxn
            int temp=n;
            n=m;
            m=temp;
        }
        
        return pos;
    }
    //水平反转仅将原来第j列变成倒数第j列。直接坐标变换就行
    private static int[] flip(int[] pos, int times){
        times=times%2;
        
        if(times==1){
            
            //pos[1]=j;
            pos[1]=m-pos[1]+1;
        }
        return pos;
    }
    
    private static int[] antiClockwise(int[] pos, int times){
        times=times%4;
        
        while(times-->0){
            
            //change arr
            int new_i=m-pos[1]+1;
            pos[1]=pos[0];
            pos[0]=new_i;
            //chang n m
            int temp=n;
            n=m;
            m=temp;
            
        }
        return pos;
    }
}
````



