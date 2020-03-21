# 文本处理

## wc

### 作用

计算文本的行数，单词数或者字节数。

### 常见用法

- 计算行数:

  wc -l file

- 计算单词数:

  wc -w file

- 计算字节数:

  wc -c file

- 计算字节数 (会考虑多字节):

  wc -m file
  
常和管道等搭配使用 ，比如 `cat ./a.js | grep 'function' | wc -l`
