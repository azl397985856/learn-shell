# 管道和重定向

## 基础

内核（kernel）利用文件描述符（file descriptor）来访问文件。 文件描述符是非负整数。 打开现存文件或新建文件时，内核会返回一个文件描述符。 读写文件也需要使用文件描述符来指定待读写的文件。linux 中一切资源都可以抽象为文件，包括硬件，比如磁盘，网卡等。

刚才说了文件描述符本质上是一个非负整数， 这里介绍三个特殊的文件描述符：

- 文件描述符 0 表示 标准输入
- 文件描述符 1 表示 标准输出
- 文件描述符 2 表示 标准错误

因此直觉上`2>1`表示的就是将标准错误重定向到标准输出。但是如果这么写的话，实际上 1 会看成是名称是 1 文件。为了消除这个误会，我们要这么写`2>&1`。 & 表示其是一个文件描述符，而不是一个文件。

## 管道

通过管道可以将一个命令的输出导入到另一个命令的输入。管道的这种使用方式并不局限于文本流，尽管这是它的最常见用法。

```bash
command1 | command2 paramater1 | command3 parameter1 - parameter2 | command4
```

在两个命令之间使用管道 | 操作符将的一个命令的 stdout 指向第二个命令的 stdin

```bash
bunzip2 -c somefile.tar.bz2 | tar -xvf -
```

> 连字符 "-" 取代文件名作为参数，表示输入来自 stdin 而不是文件。

有时候一个命令的输出，并不能很好的转化为命令行输入， 这个时候或许 xargs 就可以起到作用了

## 重定向

- \>

\> 操作符会将左边命令的输出导入到右边的文件, 如果右侧的文件是存在的，那么其会被左边命令的标准输出覆盖。

eg:

```bash
nohup /usr/local/node/bin/node test.js >> /usr/local/node/output.log 2>&1 &
```

上面会调用 node 去执行 test.js, 其标准输出会被追加到/usr/local/node/output.log， 并且标准错误输出也会被追加进去。

- \> \>

\> \> 操作符会将左边命令的输出导入到右边的文件, 如果右侧的文件是存在的，那么其会左边命令的标准输出会追加到文件末尾。

简单来说，> 和 >> 的区别可以用以下例子来说明：

```
ps -aux > log
ps -aux >> log
```

ps -aux > log 会`覆盖` log 文件。而 ps -aux >> log 会在 log 文件后面`追加`内容。

- <

相对于前面，这种用到的相对较少。

```bash
./input.sh < log
```

上面的例子会讲 log 文件内容作为参数传入到 input.sh 中。

## 参考

- [Shell Input and Output](https://developer.apple.com/library/archive/documentation/OpenSource/Conceptual/ShellScripting/ShellInputandOutput/ShellInputandOutput.html#//apple_ref/doc/uid/TP40004268-CH3-SW9)

- [What Are stdin, stdout, and stderr on Linux?](https://www.howtogeek.com/435903/what-are-stdin-stdout-and-stderr-on-linux/)
