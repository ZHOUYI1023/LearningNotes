# Find files
* `locate file` 
fast, but may need to update database first using `sudo updatedb`
* `find`
`find /etc -name “*.log”`  在/etc下查找“*.log”的文件
`find -amin -10`在系统中搜索最后１０分钟访问的文件
`find -atime -2`查找在系统中最后４８小时访问的文件
`find -mmin -5`查找在系统中最后５分钟修改过的文件
`find -mtime -1`查找在系统中最后2４小时修改过的文件
* `grep` global search regular expression(RE) and print out the line
`find /etc -name "*" | xargs grep "hello abcserver"`  
在某个路径下查找所有包含“hello abcserver”字符串的文件

# Monitor CPU
```
htop
```
---
* **u**    Show only processes owned by a specified user.
* **M**    Sort by memory usage (top compatibility key).
* **P**    Sort by processor usage (top compatibility key).
* **T**    Sort by time (top compatibility key).
---

* **PID**  The process ID.
* **PRI** Priority
* **NI** The  nice  value  of  a process, from 19 (low priority) to -20 (high priority). A high value means the process is being nice, letting others have a higher relative priority. The usual OS permission restrictions for adjusting priority apply.
* **VIRT** The size of the virtual memory of the process.
* **RES** The  resident  set  size  (text  +  data + stack) of the process (i.e. the size of the process's used physical memory).
* **SHR** The size of the process's shared pages
* **S** The state of the process:
    * S for sleeping (idle)
    * R for running
               D for disk sleep (uninterruptible)
               Z for zombie (waiting for parent to read its exit status)
               T for traced or suspended (e.g by SIGTSTP)
               W for paging
* **TIME+** The  time,  measured in clock ticks that the process has spent in user and system time
* **CPU%** The percentage of the CPU time that the process is currently using.
* **MEM%** The percentage of memory the process is currently using (based on the process's resident memory size, see M_RESIDENT above).

# Monitor GPU
```
nvcc --version 
cat /usr/local/cuda/version.txt 
```
```
watch -n 0.1 nvidia-smi
```
---

Git遇到warning: LF will be replaced by CRLF

LF和CRLF都是换行符，在各操作系统下，换行符是不一样的，Linux/UNIX下是LF,而Windows下是CRLF。

    CR：Carriage Return，对应ASCII 13中转义字符\r，表示回车
    LF：Linefeed，对应ASCII 10中转义字符\n，表示换行
    CRLF：Carriage Return & Linefeed，\r\n，表示回车并换行

(ASCII码表里也有用newline, nl表示换行的),据传说,CR、LF最原始的还要追踪到最早到机械打字机时代,CR回到同一行的纸张最左侧的意思,LF代表换一行,将纸张上一一行,两个组合就是换行。

在Git通过下面的命令配置：
```bash
$git config --global core.autocrlf true
# Configure Git on Windows to properly handle line endings
```