#### 二进制加法机


两个二进制数加法类似十进制数的加法，会产生进位，如下

```c
加法  0   1
0     0   1
1     1   0(c=1)

```

观察加法产生的结果以及进位规律：

```c
和  0   1
0   0   1
1   1   0

进  0    1
0   0    0
1   0    1
```

和的结果和异或运算一致，进位结果和与运算结果一致，因此可以将异或门和与门组合成两个一位的二进制数的加法器：

![xor-and](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/xor-and.jpg)

简化如下形式：

![half-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/half-adder.jpg)

只能计算两个一位二进制数的加法器称作半加器，它产生的结果如下：

```c
A/B 是两个相加的数  S 是和 C 是进位
A    B    S   C
0    0    0   0
0    1    1   0
1    0    1   0
1    1    0   1
```

半加器只能计算两个一位二进制数的求和运算，它会产生一个和和一个进位输出，如果要计算大于一位的二进制数的加法，就需要把两个半加器连起来。

![full-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/full-adder.jpg)

要理解它的工作原理，先从最左边第一个半加器的A 输入和B 输入开始，其输出是一个和及相应的进位。
这个和必须和前一列的进位输入(简称CI) 加起来，然后把它们输入到第二个半加器。第二个半加器的和输出是最后的和。
两个半加器的进位输出又输入到一个或门，或门产生了本次加法的进位输出。你可能会想这里还需要一个半加器，这当然是可行的。
但当你把所有的可能情况考虑完，你会发现两个进位不可能同时为1。
当两个输入不能同时为1时，或门已足够用于表示两个进位的加法，此时或门和异或门的功能是相同的。

上图可简化表示为下面的方块图，称其为“全加器（Full Adder）”：

![full-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/full-adder-1.png)
