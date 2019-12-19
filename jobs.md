# Jobs

## nohup

no hange up 的缩写，翻译为不挂起。语法：nohup COMMAND [ARG]...

假如你使用 ssh 登录了远程的 Linux 服务器，运行了一些长时间运行的任务，比如启动一个服务器。如果你退出 ssh，对应终端会关闭，终端会收到 HUP（hangup）信号从而关闭其所有子进程，这样你的服务就没了。

解决办法有两种：

1. 让进程忽略 HUP 信号
2. 或让进程运行在新的会话里从而成为不属于此终端的子进程。

有一点需要注意，无论是否将 nohup 命令的输出重定向到终端，输出都将附加到当前目录的 nohup.out 文件中。如果当前目录的 nohup.out 文件不可写，输出重定向到 \$HOME/nohup.out 文件中。如果没有文件能创建或打开以用于追加，那么 Command 参数指定的命令不可调用。

## command& 让进程在后台运行

产生一个新的子 shell 并在这个子 shell 中将任务放置到后台运行，从而不受当前 shell 终端的 HUP 信号影响。一般和 nohup 一起用。

```bash
nohup /usr/local/node/bin/node /www/im/chat.js >> /usr/local/node/output.log 2>&1 &
```

## jobs

查看正在运行的后台进程。 如果指定了 jobid 则只会查询指定的 job。

## fg 和 bg

- fg 让后台运行的进程到前台来

```bash
fg %jobid
```

- bg 让前台运行的进程到后台去

```bash
bg %jobid
```

> 其中 jobid 可以通过上面的 jobs 命令查到。

## ctrl + z

本质上发送一个信号，在这一点和 ctrl + c (SIGINT 信号)等类似。其功能是将一个前台运行的进程放到后台，并且暂停。

关于信号，你可以通过`kill -l` 查看所有的信号种类:

```bash
$ kill -l
HUP INT QUIT ILL TRAP ABRT EMT FPE KILL BUS SEGV SYS PIPE ALRM TERM URG STOP TSTP CONT CHLD TTIN TTOU IO XCPU XFSZ VTALRM PROF WINCH INFO USR1 USR2
$ kill -l | wc -w
31
```

这里给一个列表：

```
取值	名称	解释	默认动作
1	SIGHUP	挂起
2	SIGINT	中断
3	SIGQUIT	退出
4	SIGILL	非法指令
5	SIGTRAP	断点或陷阱指令
6	SIGABRT	abort发出的信号
7	SIGBUS	非法内存访问
8	SIGFPE	浮点异常
9	SIGKILL	kill信号	不能被忽略、处理和阻塞
10	SIGUSR1	用户信号1
11	SIGSEGV	无效内存访问
12	SIGUSR2	用户信号2
13	SIGPIPE	管道破损，没有读端的管道写数据
14	SIGALRM	alarm发出的信号
15	SIGTERM	终止信号
16	SIGSTKFLT	栈溢出
17	SIGCHLD	子进程退出	默认忽略
18	SIGCONT	进程继续
19	SIGSTOP	进程停止	不能被忽略、处理和阻塞
20	SIGTSTP	进程停止
21	SIGTTIN	进程停止，后台进程从终端读数据时
22	SIGTTOU	进程停止，后台进程想终端写数据时
23	SIGURG	I/O有紧急数据到达当前进程	默认忽略
24	SIGXCPU	进程的CPU时间片到期
25	SIGXFSZ	文件大小的超出上限
26	SIGVTALRM	虚拟时钟超时
27	SIGPROF	profile时钟超时
28	SIGWINCH	窗口大小改变	默认忽略
29	SIGIO	I/O相关
30	SIGPWR	关机	默认忽略
31	SIGSYS	系统调用异常
```

## setsid

set shell id 的缩写。其会在一个新的会话中运行命令，从而可以避免当前终端发出的 HUP 信号造成的影响。

## disown

如果你忘记了使用上面的方法让一个进程变成后台进程。那么可以使用 disown 为没有使用 nohup 与 setsid 的进程加上忽略 HUP 信号的功能。

使用方法：

- 将当前正在前台运行的进程放到后台运行（ctrl+z 和 bg）;
- 然后执行 disown -h %jobid

## screen

screen 是建立一个新的全屏虚拟会话终端，这个会话只有在手动输入 exit 的时候才会退出，在这个会话里执行的命令不用担心 HUP 信号会对我们的进程造成影响，因此也不用给每个命令前都加上“nohup”或“setsid”了，非常适合我们有规划的执行大量的后台任务，可以非常方便的让我们对这些后台任务进行管理。

使用方法：
screen //立即创建并进入一个会话。
screen -dmS {name} //建立一个处于断开模式下的会话，并根据我们的需要指定其会话名称。
screen -list //列出所有会话。
screen -r {name} //进入指定会话。
ctrl +ad //输入快捷键 ctrl +a 和 d，可暂时退出当前会话。
exit //进入指定会话后执行 exit 即可关闭该会话。

## 参考

- [Linux 运行与控制后台进程的方法：nohup, setsid, &, disown, screen](https://www.cnblogs.com/itech/archive/2012/09/16/2687404.html)
- [Linux 信号(signal)机制](http://gityuan.com/2015/12/20/signal/)
