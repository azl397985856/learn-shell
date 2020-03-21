# 文本处理

## wc

### 作用

计算文本的行数，单词数或者字节数。

### 常见用法

- Count lines in file:
  wc -l file

- Count words in file:
  wc -w file

- Count characters (bytes) in file:
  wc -c file

- Count characters in file (taking multi-byte character sets into account):
  wc -m file
  
常和管道等搭配使用 ，比如 `cat ./a.js | grep 'function' | wc -l`
