Windows命令行：背景知识
======================

这是这个系列文章的第一篇。在这个系列文章里，我们将会探索有关命令行的方方面面。从命令行的前生今世，到我们正在如何改造并将Windows控制台和命令行现代化。

在系列“Windows命令行”里的文章：
---------------------------
> **1. 背景知识** [这篇文章]<br>
> 2. Windows命令行的演变过程<br>
> 3. 在Windows控制台背后<br>
> 4. 介绍Windows伪控制台 (PseudoConsole, ConPTY)<br>
> 5. Unicode 和 UTF-8 输出文本缓存<br>



不管你是一个经验丰富的老兵，还是初来乍到计算机领域（非常欢迎），希望你能发现这个系列的文章非常有趣，并且有丰富的信息。所以，泡一杯咖啡，准备好到命令行的起源之处来一次旋风之旅吧！

在很久很久以前的一间机房内.....
----------------------------------

在电子计算的早期，人们需要一种有效的方法向计算机发送指令和数据，并且能够看到他们的指令和计算的结果。

电传打字机（Teletype）是最早出现的高效的人机交互接口之一。电传打字机是一个带有键盘用于给用户输入的电子设备，并且带有某种输出设备用以显示结果—————早期是打印机，后来被屏幕取代。

操作员输入的字符将在本地缓存，并且以信号的形式沿着电缆（比如RS-232电缆），按每秒10个字符（或者说，110bps）从电传打印机发送到小型或者大型计算机上。

![command-line-backgrounder-teletype](https://github.com/kernelbin/Article-WindowsCommandLine-ZHCN/blob/master/command-line-backgrounder-teletype.jpg?raw=true)

> David Gesswein 超赞的[网站](https://www.pdp8.net/) 有很多有关[ASR33](https://www.pdp8.net/asr33/asr33.shtml)（以及PDP-8与其相关技术）的更多信息，包括照片，视频等。计算机上的程序将接收到输入的字符，并且决定如何处理它们，并且可以选择异步的将字符回传给电传打印机。电传打印机将会将显示或者打印出回传的字符，以便操作员做出回应。

在随后的几年中，这项技术得到了改进，将传输速度提高到19,200bps，并用一个阴极射线管（CRT）显示器取代了先前嘈杂且操作麻烦的打印机。这种阴极射线管显示器通常与80年代和90年代的计算机终端相关联，比如无处不在的DEC VT100终端：

![command-line-backgrounder-vt100-terminal](https://github.com/kernelbin/Article-WindowsCommandLine-ZHCN/blob/master/command-line-backgrounder-vt100-terminal.jpg?raw=true)

尽管技术在不断改进，这种终端向运行在计算机上的程序发送字符，计算机通过文本输出向用户作出响应的模式却保留了下来，并且留存至今，仍是所有平台上所有命令行和终端的交互模式的根基！

![command-line-backgrounder-command-line-terminal](https://github.com/kernelbin/Article-WindowsCommandLine-ZHCN/blob/master/command-line-backgrounder-command-line-terminal.png?raw=true)

这个模型十分优雅的原因之一是，这个系统中的每一个组存部分都始终保持简单和一致性： 键盘输出的字符被缓存下来，并且以电信号发送给与之连接的电脑。输出设备简单的将计算机输出的字符打印到显示设备上（比如，纸张或是屏幕上） 。

并且由于这个系统的每一组成部分都与下一个组成部分通过简单的传递字符流来通信，所以引进不同的通信设施变得相对简单，比如添加一个调制解调器（Modem，猫）使得输入输出字符流可以通过电话线远距离传输。
