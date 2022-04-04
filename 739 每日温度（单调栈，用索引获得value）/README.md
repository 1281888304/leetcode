做过很多次，单调栈经典题目，忘记了可以用下标index获取value，就没必要存两个stack了

<img width="531" alt="Screen Shot 2022-04-04 at 12 43 31 PM" src="https://user-images.githubusercontent.com/59748598/161619908-927711e4-c2f3-4594-9801-047256f8cd1a.png">

然后用LinkedList或者Deque的实现类ArrayDeque来代替stack，就用LinkedList好了

两种方法：
```` 
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int len=temperatures.length;
        int[] dp=new int[len];
        //Deque<Integer> stack=new ArrayDeque<>();
        LinkedList<Integer> stack=new LinkedList<>();
        //stack.push(temperatures[0]);
        for(int i=0;i<len;i++){
            int curTemp=temperatures[i];
            while(!stack.isEmpty() && curTemp>temperatures[stack.peek()]){
                int index=stack.pop();
                dp[index]=i-index;

            }
            stack.push(i);
        }
        return dp;
    }
}
````

双stack垃圾方法
```` 
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int len=temperatures.length;
        int[] dp=new int[len];

        LinkedList<Integer> stackVal=new LinkedList<>();
        LinkedList<Integer> stackIndex=new LinkedList<>();
         stackVal.push(temperatures[0]);
        stackIndex.push(0);

        for(int i=1;i<len;i++){
            int val=temperatures[i];
            if(val<=stackVal.peek()){
                stackVal.push(val);
                stackIndex.push(i);
            }
            else{
              
              while(!stackVal.isEmpty() && !stackIndex.isEmpty() && val>stackVal.peek()){
                  int index=stackIndex.pop();
                  dp[index]=i-index;
                  stackVal.pop();
              }
              stackVal.push(val);
              stackIndex.push(i);  
            }
        }
        return dp;
        
    }
}


````





