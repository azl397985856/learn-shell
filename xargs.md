# xargs

## 简介

xargs 可以读 stdin 的数据，以空格符或断行字符分割，将 stdin 的数据分割成为 若干个 arguments 。

有些命令的输出并不能直接作为命令行参数，也就说是不支持管道命令，比如`pgrep process_name`。如下：

> pgrep 命令以名称为依据从运行进程队列中查找进程，并显示查找到的进程 id。

```bash

pgrep progress_name | kill

```

上述的命令是不行的。 如果想要达到效果，一个方法就是借助于 xargs， 它可以将命令输出转化为可以标准输入，支持多种格式。

```bash
pgrep process_name | xargs kill
```

## 常用用法

Execute a command with piped arguments coming from another command, a file, etc.
The input is treated as a single block of text and split into separate arguments on spaces, tabs, newlines and end-of-file.

- Main usage pattern:
  arguments_source | xargs command

- Delete all files with a .backup extension. -print0 on find uses a null character to split the files, and -0 changes the delimiter to the null character (useful if there's whitespace in filenames):
  find . -name '\*.backup' -print0 | xargs -0 rm -v

- Execute the command once for each input line, replacing any occurrences of the placeholder (here marked as _) with the input line:
  arguments_source | xargs -I _ command \_ optional_extra_arguments

- Parallel runs of up to max-procs processes at a time; the default is 1. If max-procs is 0, xargs will run as many processes as possible at a time:
  arguments_source | xargs -P max-procs command
