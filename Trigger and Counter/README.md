#### 振荡和计数器

继电器输出同时又作为自己输入，做如下连接，只要开关是闭合的，金属簧片就会上下跳动—使电
路闭合或断开—并制造一种声音。如果金属簧片制造了一种刺耳的声音，它就构成了一个
蜂鸣器。如果金属簧片附上一把小锤子，再加一个金属锣，它就构成了一个电铃。

![oscillator](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/relay.png)

也可以像这样表示：

![oscillator](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/oscillator.jpg)

对于反向器而言，当输入为0时，输出为1；输入为1时，输出为0。在该电路中闭合开关
会使反向器中的继电器间断地闭合和断开。如果去掉开关，可以使反向器连续地工作

![oscillator](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/oscillator-no-switch.jpg)

这幅图似乎在演示一种逻辑矛盾，反向器的输出是和其输入相反的，但是在这里，其输
出同时又是其输入。需要特别指出的是，反向器实际上是一个继电器，而继电器从一个状态
转换到另一个状态是需要时间的。所以，即使输入和输出是相等的，输出也会很快地改变，
成为输入的倒置（当然，随即输出也就改变了输入，如此反复）。
电路的输出是什么呢？其实就是提供电压和不提供电压之间的变换。或者说输出要么是0，
要么是1。

这个电路称为`振荡器`，它和我们以前见到的每样东西都有本质上的区别。以前，所有的
电路都靠手动地断开或闭合开关来改变状态，而振荡器却不需要人的干涉，它可以自主地工
作。

当然，单独的一个振荡器不会有什么用，但在本章的后面及接下去的几章里，你会看到
这个电路和其他电路连接后构成了自动控制中一个十分关键的部分。所有计算机都靠某种振
荡器来使其他部件同步工作。

振荡器的输出是0和1的交替序列，可以用下图形象地来表示它：

![sequence](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/oscillator-sequence.jpg)

图中，水平轴表示时间，垂直轴表示输出是0或1.

此图表示随着时间的变化，振荡器的输出在0和1之间交替变化。基于这个原因，振荡器
有时称为时钟（c l o c k），因为通过对振荡次数记数还可确定时间。

那么，振荡器运行的速度有多快呢？也就是说，金属簧片上下跳动的频率是多少？每秒
有多少次呢？很明显，这依赖于继电器是如何构造的。容易想到，一个大的、笨重的继电器
只能迟钝地上下摆动；而一个小的、轻巧的继电器可以迅速地跳动。
我们把振荡器从某个时间的输出开始，经历一段变化又回到同样输出的这一段间隔称为
振荡器的一个循环（c y c l e）：

![cycle](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/oscillator-cycle.jpg)

一个循环所需要的时间称为振荡器的周期。假设一个振荡器的周期是0 . 0 5秒，则可以在水
平轴上标出时间：

![frequence](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/oscillator-freq.jpg)

振荡器的频率是周期的倒数。本例中，若振荡器的周期是0 . 0 5秒，则其频率是1÷0 . 0 5秒，
即每秒钟2 0个循环。这表明振荡器的输出每秒钟改变2 0次。我们可以说这个振荡器的频率是2 0赫兹，或直接简写为2 0 H z。

到目前为止，我们只是在假设一个振荡器的速度。到本章末尾，我们可以构造一种器件
来真正地测量一个振荡器的速度。
为了构造这个器件，先看一个用特殊方式连接的一对或非门。或非门的特点是只有两个
输入都为0时，输出才为1：

![nor](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/nor-values.jpg)

下图是含有两个或非门、两个开关和一个灯泡的电路：

![two-nor-gates](https://github.com/deanisty/Electron/blob/master/Trigger%20and%20Counter/two-nor-gates.png)

注意图中奇特的连接方式：
