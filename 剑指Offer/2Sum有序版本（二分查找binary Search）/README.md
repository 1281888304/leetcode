https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/

<img width="525" alt="Screen Shot 2022-03-19 at 12 44 47 PM" src="https://user-images.githubusercontent.com/59748598/159136121-7f00d2a4-73a7-4164-abc7-02c8f5383b62.png">

因为这里肯定会有答案，所以我们设立left指针和right指针

一个在最左边，一个最右边。如果sum==target就返回，如果sum>target，right指针--，sum<target,left指针++

因为答案肯定有一个，所以说while(i<j)最后i不会等于j，最坏的结果就是j=i+1

```` 
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        for (int i = 0, j = numbers.length - 1; i < j;) {
            int sum = numbers[i] + numbers[j];
            if (sum == target) return new int[] {i + 1, j + 1};
            else if (sum > target) j--;
            else i++;
        }
        return null;
    }
}
````






