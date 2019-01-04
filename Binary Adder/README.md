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

下表是全加器所有可能的输入以及相应的输出：

```c
A/B 是两个相加的数  S 是和 CI 是进位输入  CO 是进位输出
A   B    CI    S    CO
0   0    0     0    0
0   1    0     1    0
1   0    0     1    0
1   1    0     0    1
0   0    1     1    0
0   1    1     0    1
1   0    1     0    1
1   1    1     1    1
```

有了全加器之后，就可以实现任意位数的二进制求和运算了，方法就是把全加器组合起来使用，最低位的全加器的进位输入始终为0，因为它前面没有全加器给它进位，
所以进位输入接地，然后第一个全加器的进位输出作为第二个全加器的进位输入，以此类推，最高位的全加器的进位输出作为最后加法结果的进位位，这样组合起来的
加法器如下图所示：

![8-bit-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/8-bit-adder.png)

或者画成这样：

![8-bit-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/encap-8-bit-adder.png)

也可以封装在小盒子里：

![8-bit-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/encap-8-bit-adder.png);

一旦构造了一个8位加法器，就可以构造另一个加法器。把它们级联起来可以很容易地构成1 6位加法器：

![16-bit-adder](https://github.com/deanisty/Electron/blob/master/Binary%20Adder/images/16-bit-adder.jpg)

右边加法器的进位输出连到左边加法器的进位输入端。左边加法器的输入包含了两个加数的高8位，同时产生了结果的高8位。

现在，你可能会问：“计算机真的是以这种方式把数字加起来的吗？”
基本上是这样的，但不完全是。

首先，加法器应该做得更快。如果你明白这个电路是如何工作的，你会看到最低位相加产生的进位作为下一列数相加的一个输入，
而第3列的加法又等着第2列加法的进位，依此类推。加法器总体的速度等于加数的位数乘以单个全加器的速度。这种进位方式称为行波进位。
更快的加法器使用称为先行进位的加法电路，从而加快了加法进程。

第二（但是十分重要），计算机再也不用继电器了！尽管它们曾经用过。
建于2 0世纪3 0年代初的第一批数字计算机使用继电器，后来又用了真空管。现代计算机用晶体管。
当用在计算机中时，晶体管和继电器的功能差不多，但是晶体管速度更快，体积更小，更安静，更省电，而且还便宜不少。
构造一个8位加法器仍然需要1 4 4个晶体管（如果采用先行进位，则需要更多），但整体电路的体积却小多了。

