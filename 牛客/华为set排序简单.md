


链接：https://www.nowcoder.com/questionTerminal/3245215fffb84b7b81285493eae92ff0?answerType=1&f=discussion
来源：牛客网



                                                       ```` 
```` 
import java.util.Scanner;
import java.util.Set;
import java.util.TreeSet;
 
public class Main{
    public static void main(String [] args){
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            int size = scanner.nextInt();
            Set<Integer> numberSet = new TreeSet<>();
 
            for (int i = 0; i < size; i++) {
                numberSet.add(scanner.nextInt());
            }
            numberSet.forEach(System.out::println);
        }
    }
}
````








