![Screen Shot 2022-04-27 at 10 36 52 PM](https://user-images.githubusercontent.com/59748598/165683566-c659da76-86d2-46f0-842a-032871ad993c.png)


![Screen Shot 2022-04-27 at 10 37 00 PM](https://user-images.githubusercontent.com/59748598/165683584-12bafa67-9b47-49e5-b7b1-04e5bc2fd534.png)

用Long.toBinaryString(a);

a是一个long

integer也有这个功能

<img width="468" alt="Screen Shot 2022-09-01 at 6 15 45 PM" src="https://user-images.githubusercontent.com/59748598/188038785-c64b51eb-cf29-4a69-9853-888dbb449c0e.png">

Decmial：十进制

heptad：七进制


hexadecimal： 16进制

Octal：八进制

一个integer就是可以换成多个进制，integer不是进制，是integer可以转成多个进制

3 二进制： 0011
 十进制：3
 
 
<img width="710" alt="Screen Shot 2022-09-01 at 7 14 30 PM" src="https://user-images.githubusercontent.com/59748598/188044275-65a17f97-32d2-4fbb-91d0-208ce50773d6.png">

这里判断long有多少个1，也很好判断，每次和比自己小1的判断，去除掉一个1，看可以去多少次。and操作比如1111 和 1110 and &完编程1110

1110 和1101 and完编程1100 以此类推，每次res+1
