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

## sort

### 作用

### 常见用法

对文本内容按行进行排序
```
- 升序排序:
  sort filename

- 降序排序:
  sort -r filename

- 忽略大小写:
  sort --ignore-case filename

- 按数字大小排序，而不是按字母表顺序排序:
  sort -n filename

- 去重:
  sort -u filename

```
## uniq

### 作用

 Output the unique lines from the given input or file.
  Since it does not detect repeated lines unless they are adjacent, we need to sort them first.

### 常见用法
```
- 每一行最多显示一次:
  sort file | uniq

- 仅显示出现一次的行:
  sort file | uniq -u

- 仅显示出现多次的行:
  sort file | uniq -d

- 显示出现次数:
  sort file | uniq -c
```
## awk

### 作用

多功能文本处理工具，参考 https://github.com/onetrueawk/awk

### 常见用法
```
- Print the fifth column (a.k.a. field) in a space-separated file:
  awk '{print $5}' filename

- Print the second column of the lines containing "something" in a space-separated file:
  awk '/something/ {print $2}' filename

- Print the last column of each line in a file, using a comma (instead of space) as a field separator:
  awk -F ',' '{print $NF}' filename

- Sum the values in the first column of a file and print the total:
  awk '{s+=$1} END {print s}' filename

- Sum the values in the first column and pretty-print the values and then the total:
  awk '{s+=$1; print $1} END {print "--------"; print s}' filename

- Print every third line starting from the first line:
  awk 'NR%3==1' filename

- Print all values starting from the third column:
  awk '{ s = ""; for (i=3; i <= NF; i++) s = s $i " "; print s }'

- Print different values based on conditions:
  awk '{if ($1 == "foo") print "Exact match foo"; else if ($1 ~ "bar") print "Partial match bar"; else print "Baz"}'
  ```
