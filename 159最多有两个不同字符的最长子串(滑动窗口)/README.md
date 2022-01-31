<img width="519" alt="Screen Shot 2022-01-31 at 3 11 47 PM" src="https://user-images.githubusercontent.com/59748598/151888306-0b7ba0f0-209a-4120-a9cd-50e8fba48f2f.png">

只能有两个character字符，大概是set/map，算法逻辑是一旦有新的加进来size超过三，滑动窗口算法保证每次滑动窗口都是满足只有两个

eceba的时候，只要往set里面添加size不超过二，left不动，超过了比如说到b这里，从e开始往回找新的left，

ccaabbb到b的时候，新的left是第一个a index=2

![image](https://user-images.githubusercontent.com/59748598/151888508-65e07366-bb75-4256-a416-efe948043660.png)






