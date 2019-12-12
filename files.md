# Files

All thing are files in linux. data, network eg `tcp` or `udp` , even hardware are files.

A file descriptor is a number that uniquely identifies an open file in a computer's operating system. It describes a data resource, and how that resource may be accessed.

## lsof

`lsof` is short for `list open files`, just like its name, `lsof` will list the files opened currently.

`lsof` Lists open files and the corresponding processes.
Note: Root privileges (or sudo) is required to list files opened by others.

### commands

- Find the processes that have a given file open:
  lsof path/to/file

- Find the process that opened a local internet port:
  lsof -i :port

- Only output the process ID (PID):
  lsof -t path/to/file

- List files opened by the given user:
  lsof -u username

- List files opened by the given command or process:
  lsof -c process_or_command_name

- List files opened by a specific process, given its PID:
  lsof -p PID

- List open files in a directory:
  lsof +D path/to/directory

- Find the process that is listening on a local TCP port:
  lsof -iTCP:port -sTCP:LISTEN

- [每天一个 linux 命令（51）：lsof 命令](https://www.cnblogs.com/peida/archive/2013/02/26/2932972.html)
- [lsof command in Linux with Examples](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/)

### FD types

- cwd for current working directory
- txt
- lnn
- er for error
- jld for jail directory
- ltx for shared library text (code and data)
- mxx
- m86
- mem
- mmap
- pd
- rtd
- tr
- v86
- 0
- 1
- 2
