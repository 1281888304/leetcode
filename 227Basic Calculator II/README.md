这道题的关键就是默认每一层stack都是相加的，然后如果是负数，就把负号push进去
精华是先设定一个初始的符号是+
然后如果遇到了 * ｜｜ /
如果碰到四个符号，就往stack里面push value
就把之前那个pop出来计算完再放回去
关键点在于如果到了最后一步（i==len-1），记得把他push进去


<img width="601" alt="Screen Shot 2022-01-08 at 1 53 25 PM" src="https://user-images.githubusercontent.com/59748598/148661186-25f1483f-8e58-40db-94d7-e7315f538433.png">


class Solution {
    public int calculate(String s) {

        if (s == null || s.isEmpty()) return 0;
        int len = s.length();
        Stack<Integer> stack = new Stack<Integer>();
        int currentNumber = 0;
        char operation = '+';
        for (int i = 0; i < len; i++) {
            char currentChar = s.charAt(i);
            if (Character.isDigit(currentChar)) {
                currentNumber = (currentNumber * 10) + (currentChar - '0');
            }
            if (!Character.isDigit(currentChar) && !Character.isWhitespace(currentChar) || i == len - 1) {
                if (operation == '-') {
                    stack.push(-currentNumber);
                }
                else if (operation == '+') {
                    stack.push(currentNumber);
                }
                else if (operation == '*') {
                    stack.push(stack.pop() * currentNumber);
                }
                else if (operation == '/') {
                    stack.push(stack.pop() / currentNumber);
                }
                operation = currentChar;
                currentNumber = 0;
            }
        }
        int result = 0;
        while (!stack.isEmpty()) {
            result += stack.pop();
        }
        return result;
    }
}

