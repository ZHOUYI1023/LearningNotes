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