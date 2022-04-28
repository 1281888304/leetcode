https://blog.csdn.net/u022812849/article/details/107142652?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165111747716782391851625%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165111747716782391851625&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-107142652.142^v9^pc_search_result_cache,157^v4^control&utm_term=%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F&spm=1018.2226.3001.4187


把原是数组看成矩阵，按列来排序，最上面的就是最小的.每一列用插入排序法insert


![Screen Shot 2022-04-27 at 8 47 36 PM](https://user-images.githubusercontent.com/59748598/165672446-0a911760-b4ae-4a72-a432-d02b73815722.png)

原始n=16，分成8列

 然后分出4列
 
 ![Screen Shot 2022-04-27 at 8 48 07 PM](https://user-images.githubusercontent.com/59748598/165672497-d3cd4c91-d9b4-4b2d-b77c-2e7ca166cb35.png)


两列
![Screen Shot 2022-04-27 at 8 48 37 PM](https://user-images.githubusercontent.com/59748598/165672534-a1d48d70-d01e-479e-b721-d8d1309dc9bb.png)


一列结果
![Screen Shot 2022-04-27 at 8 49 06 PM](https://user-images.githubusercontent.com/59748598/165672571-7d30bff4-024c-4d8e-a48b-45fc0943c7e2.png)

最好情况是步长序列只有1，且序列几乎有序，时间复杂度为O(n)。最好的情况下序列只有1一个元素，最好的排序时间是O(n)

希尔本人给出的步长序列，最坏情况时间复杂度是 O(n^2)。

