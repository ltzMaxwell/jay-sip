# jay-sip
Automatically exported from code.google.com/p/jay-sip


support G.711,G.722,speex

third libs in 'Downloads' Tab

搞了将近一个月的时间，将Speex的编码和解码做好了，发现还不错。

参考API，又尝试了回音消除，发现最新版还提供了用于在多线程中的playback()和capture()，有了这两个函数，就可以避免在线程中不能同步的问题。

结果，发现虽然进行了回音有了部分消除，但是，还是会一点啸叫以及回声，想来还是要做一点处理，譬如去噪，减小播放或者来音的增益。

在使用了speex提供的 preprocessor 函数后 ，原以为会更好的消除噪声，可视发现也没什么变化，反而可能会更弱，这是为什么

Update:5//12

在使用了Speex回声消除之后，以及添加了预处理的一些Api，并且优化了程序的结构，例如在接收数据然后用来播放的过程中，使用了Ringbuffer来保证数据包处理质量。

最后的结果：

1两个手机都打开扬声器 且放到最大，在不同的房间里，能够听到一声回声，即喂……喂

2两个手机不开扬声器，正常通话音量，在不同的房间里，没有回声。

因为最近比较忙，在做android上，Sip的实现内容，所以没时间贴出具体的语音处理传送项目的实现原理和步骤，等过段时间一定补上，如果有疑问，我也尽量回答

Update: 3/11

看了这篇文章：http://blog.csdn.net/zblue78/article/details/5841357 ，发现我的参数设置错误了

前几天,试了一下，把预处理里面的几个语音预处理功能都打开了，譬如去噪，VAD，结果发现确实效果不错，在没有人音的时候，确实噪声被去掉了，不过，

以前没有延时，因为加了很多处理，所以增加了开销，所以有了500ms的延时（或许吧）。 回音还是会有一点，可能还是参数设置和同步队列的问题。期待解决

Update: 12/8/2012

很多朋友加我QQ询问是否可以提供SPEEX回音消除的代码或者如何使用回音消除，很抱歉，最近由于在写论文，因此没有时间回答各位的问题，等我将论文搞定，会把相关的设计思路与使用方法公布于网上，以供大家学习与交流，如果有问题，希望以邮件给来信，将问题写清楚，我会认真回复的

UPDATE: 3/8/2013

因为毕设已经完成，论文也送审了，所以，实现诺言，将我的代码共享。共享的项目为SIP电话，包含JSIP协议栈、语音编码库（G.711、G.722、Speex），语音处理(Speex）。代码仅做测试与研究所用，如果有疑问，欢迎大家一起讨论

使用方法：首先点击init按钮，负责初始化SIP，接着可以注册SIP账户，选择呼叫对方用户，当对方接通，然后就可以打开MediaService，调用语音服务，进行语音通信
