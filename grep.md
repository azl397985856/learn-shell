# grep

grep 会寻找由换行符分隔的模式，并且 grep 打印与模式匹配的每一行。

语法：

```bash
grep "some string" file
```

## 常用用法

```
Matches patterns in input text.Supports simple patterns and regular expressions.

  - Search for an exact string:
    grep search_string path/to/file

  - Search in case-insensitive mode:
    grep -i search_string path/to/file

  - Search recursively (ignoring non-text files) in current directory for an exact string:
    grep -RI search_string .

  - Use extended regular expressions (supporting ?, +, {}, () and |):
    grep -E ^regex$ path/to/file

  - Print 3 lines of [C]ontext around, [B]efore, or [A]fter each match:
    grep -C|B|A 3 search_string path/to/file

  - Print file name with the corresponding line number for each match:
    grep -Hn search_string path/to/file

  - Use the standard input instead of a file:
    cat path/to/file | grep search_string

  - Invert match for excluding specific strings:
    grep -v search_string
```

![](https://tva1.sinaimg.cn/large/006tNbRwly1ga6goydmxdj30xc0l0teh.jpg)

> 另外，变体程序 egrep 和 fgrep 的作用与 grep -E 和 grep -F 是一样的, egrep 和 fgrep 已被弃用。
