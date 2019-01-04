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
