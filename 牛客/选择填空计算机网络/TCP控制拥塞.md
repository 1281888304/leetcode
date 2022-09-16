<img width="433" alt="Screen Shot 2022-05-11 at 9 43 38 AM" src="https://user-images.githubusercontent.com/59748598/167903181-65ae756b-ca33-4de2-a6b3-d19b76506763.png">

拥塞控制的四种算法：慢开始、拥塞避免、快重传、快恢复

1 慢开始：发一个没有出现超时重传，下一次更快，直到>设置的阀值(24)

![Screen Shot 2022-09-15 at 10 22 38 PM](https://user-images.githubusercontent.com/59748598/190562592-34e959f6-65a7-407a-9938-428ef75bb565.png)

2 拥塞避免： 发现超时重传，降低传输速度（不会直接降到开启时慢开始1），又以慢开始的方式慢慢加

![Screen Shot 2022-09-15 at 10 29 13 PM](https://user-images.githubusercontent.com/59748598/190563358-e9677055-2425-42a8-9b1c-8d86150bfe5f.png)

3 快重传+快恢复： 接受方收不到数据包，数据包丢失，重新设置cwnd，和阈值sstresh，重新执行慢开始


![Screen Shot 2022-09-15 at 10 29 04 PM](https://user-images.githubusercontent.com/59748598/190563337-902574df-9def-4421-b0d9-0ebeb7138307.png)


总结： 234都是基于不行了就重来慢开始的玩法
