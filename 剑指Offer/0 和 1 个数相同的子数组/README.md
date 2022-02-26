https://leetcode-cn.com/problems/A1NYOS/

<img width="558" alt="Screen Shot 2022-02-26 at 11 41 36 AM" src="https://user-images.githubusercontent.com/59748598/155856854-a95bf47d-3c6c-4ac1-a0fb-2b96b18b80b7.png">


解决办法就是用前缀和，用map key是sum，value是index（里当前i最远的sum）

把所有的0变成-1，如果遇到相同的，就用当前index减去最远的

![image](https://user-images.githubusercontent.com/59748598/155856973-0a387387-6a3a-463d-9bae-b5bcf5a9149a.png)

如果当前的sum之前有了，不要变，存着还是之前最远的，然后用当前i减去存着的最远的index

 
```` 
class Solution {
    public int findMaxLength(int[] nums) {
        int n=nums.length;
        int[] nums2=new int[n];
        for(int i=0;i<n;i++){
            nums2[i]=nums[i]==1 ? 1 :-1;
        }

        int sum=0;
        Map<Integer,Integer> map=new HashMap<>(); //presum
        map.put(0,-1);
        int max=0;
        for(int i=0;i<n;i++){
            sum+=nums2[i];
            if(!map.containsKey(sum)){
                map.put(sum,i);
            }
            else{
                int start=map.get(sum);
                max=Math.max(i-start,max);
            }
        }
        return max;
    }
}
````






