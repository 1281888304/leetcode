
<img width="644" alt="Screen Shot 2022-01-14 at 10 18 25 PM" src="https://user-images.githubusercontent.com/59748598/149611512-c370c512-784a-4496-9992-daa5e7f9ca9b.png">
这道题也属于经典，首先是要创建一个只读集合

然后在下面回溯的时候，通过index/start找到这个号码对应的三个或者四个数字，开始添加，然后往下一个数字走，回来的时候撤销这个操作，顺着for loop把这个号码第二个数字找到然后再往后走

比如说23 先拿到ad然后回溯（走失败了），把d撤销，拿到e变成ae，到了最后3这个数字对应的全部都加完了，就回溯到2，把a取消，加上b，以此类推，也是为什么答案从a到c顺序完整

class Solution {

//只读集合
private Map<Character, String> map = Map.of(
    '2', "abc", '3', "def", '4', "ghi", '5', "jkl", 
    '6', "mno", '7', "pqrs", '8', "tuv", '9', "wxyz");

public List<String> letterCombinations(String digits) {
     List<String> result = new ArrayList<>();
    if(digits.length()==0){
        return result;
    }
    
    backTracking(0,new StringBuilder(),digits,result);
    return result;
}
private void backTracking(int start, StringBuilder sb,String digits,
                         List<String> result){
   
    if(sb.length()==digits.length()){
        result.add(sb.toString());
        return;
    }
    
    String s=map.get(digits.charAt(start));
    for(char c : s.toCharArray()){
        sb.append(c);
        backTracking(start+1,sb,digits,result);
        sb.deleteCharAt(sb.length()-1);
    }
}
}
