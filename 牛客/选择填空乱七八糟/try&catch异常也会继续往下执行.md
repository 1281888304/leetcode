
![Screen Shot 2022-04-29 at 10 46 29 PM](https://user-images.githubusercontent.com/59748598/166093229-630b5d96-20f8-4dbe-aad5-b3d7d0b4b11c.png)

![Screen Shot 2022-04-29 at 10 46 37 PM](https://user-images.githubusercontent.com/59748598/166093234-939e9043-e804-4f9f-addb-c3e15bac32ef.png)


当执行a/b的时候就会被范围更小且位于最前面的ArithmeticException异常捕获，因此try不会再打印，下面范围更大的Exception块也不会再执行

1 范围最小的普货到了，更大的就不会欧货。另一种说法是前面先抓铺，后面就不需要了（抓完了）

2 会继续执行打印end


