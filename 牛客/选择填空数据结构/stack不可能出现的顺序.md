<img width="908" alt="Screen Shot 2022-04-25 at 1 53 44 AM" src="https://user-images.githubusercontent.com/59748598/165055225-62f5ba1e-b639-41e0-9025-b953cee3390f.png">

这里要考虑分批压入

说一下自己的想法吧，这种题目就是从上到下逐个排除。

A选项：先压入ABC，再压入D，弹出D；再压入E，弹出E；再压入F，弹出F；再依次弹出CBA，满足入栈顺序，所以出栈顺序为DEFCBA。

B选项：先压入AB,再压入CD，弹出DC；再压入E，弹出E；再压入F，弹出F；再依次弹出BA，满足入栈顺序，所以出栈顺序为DCEFBA。

C选项：这个选项不再赘述，因为是入栈顺序的倒序，全部一起进，一起出，所以出栈顺序为DCEFBA。

D选项：先假设弹出的FE是正确的，但是出栈时C出现在D的前面，因为C一定是比D先入栈的，所以D先出栈，选项错误，选D

E选项：与入栈顺序一致，所以是入一个，弹出一个，满足入栈顺序，所以出栈顺序为ABCDEF。

F选项：先压入A,弹出A，再压入BCD，弹出DCB；再压入EF，弹出FE，满足入栈顺序，所以出栈顺序为ADCBFE。

选项太多，就不画图了，如有说的不妥的地方，望指正，谢谢！

发表于 2020-06-03 20:41:15


