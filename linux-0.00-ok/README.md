《Linux内核完全剖析》这本书在第4章给出了一个简单多任务内核示例程序，我们称之为Linux 0.00系统。本文介绍了一种把它跑起来的方法。

# 一、实验环境
* compile system  
  ubuntu-16.04.5-desktop-i386.iso  
* bochs  
  Bochs x86 Emulator 2.6  

# 二、源码下载

下载地址是   
http://oldlinux.org/Linux.old/bochs/   
要下载的文件是linux-0.00-050613.zip   

# 三、编译

```
nick@nick-VirtualBox:~/oldlinux/linux-0.00-ok$ make
as86 -0 -a -o boot.o boot.s
ld86 -0 -s -o boot boot.o
as --32   -o head.o head.s
ld -m elf_i386 -Ttext 0 -e startup_32 -s -x -M   head.o  -o system > System.map
dd bs=32 if=boot of=Image skip=1
16+0 records in
16+0 records out
512 bytes copied, 0.00150062 s, 341 kB/s
objcopy -O binary system head
cat head >> Image
```

# 四、运行

进入虚拟机(需要有界面显示)执行

```
bochs -f bochsrc-0.00.bxrc
```

![linux-0.00运行结果](https://github.com/nicklgw/oldlinux/blob/master/linux-0.00-ok/result.png?raw=true)

# 五、参考

Linux 0.00 的编译和运行  
https://blog.csdn.net/longintchar/article/details/78757065
