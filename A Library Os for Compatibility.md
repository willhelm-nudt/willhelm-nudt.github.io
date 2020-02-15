# THE PAL ABI

_Platform Translation Layer_

Graphene目前在PAL ABI中定义了40个调用，足以支撑library OS开发所需要的主机抽象。本文中PAL ABI的主机**host**是一个OS或者一个Hypervisor这类可以支持应用程序运行的功能集合。

**Porting Simiplicity**

1.reduce size and complexity of host OS features that OS developers have to implement.

2.PAL ABI模仿类似POSIX 宏核OS的通用系统API，将调用直接转换成类似的主机抽象。例如，StreamRead()和StreamWrite()与Linux等系统的read()和write() 以及windows 系统的readfile()和writefile()类似。

**Sufficiency for Library OS Development**

简化语义相同，抽象类似的函数。例如VirtMemAlloc()与mmap()的功能相同，可以同时满足mmap()和brk()两个函数的功能。

**Migration**

Library OS保留 检查点和转移运行中的应用的VM具有的特性。进程转移是模拟写时拷贝分支的一个关键。
### PAL 调用定义

_Streams_,_Memory_,_Threads & scheduling_,_Process_,_Miscellaneous_,_RPC_

### Host-Enforced Security Isolation

同一个主机上运行的互不可信应用需要强隔离。对于可信的主机OS，可以将安全隔离交给主机代理。

同一个应用中的进程在一个沙箱中运行。多个OS库实例在一个沙箱内协同运行，从应用程序角度来看是一个统一的系统。阻挡沙箱之间的RPC流来控制。

**Thread Model**

## The library OS
### Architecture
### Multi-Process Abstractions

ex:PID,对单进程应用来说，getpid()返回的确定的值。
采用的基本抽象：将每一个LOS实例看做一个进程，在一组LOS中共享POSIX实现。（treat each library OS instance as a process and distribute the shared POSIX implementation across a collection of library OSes.）
multiple library OSes in multiple picoprocess collaborate to implement shared abstractions.pipe like RPC streams to communicate betwenn processes.

# The Host ABI
## PAL Calling Convention
partially adopt x86-64 Linux convention to simplyfy the dynamic link between the application,library OS and PAL.

**Host Differences**
PAL tranlates the calling convention between the host ABI and a system interface on the host.also resolve calling convention inconsistency.

**Error Code**
a PAL delivers the failure of a PAL call as an exception,so that the library OS can assign a handler to capture the failure.

**Dynamic Linking vs Static Linking**

ensure complete reuse of an unmodified application,as well as unmodified library OS.without modification and recompilation.

## The PAL ABI

### Stream I/O

(1)storage (2)network (3)RPC
抽象：byte stream
### Page Management
抽象：虚拟内存区域 virtual memory area(VMA)

两种方式：a file-backed VMA,created by StreamMap();an anonymous VMA,created by VirtMemAlloc()

### CPU Scheduling

focus on defining host ABIs for CPU scheduling features essential to application usability.

_creating or terminating a thread_,_scheduing a thread_,_scheduling primitives_,_waiting for scheduling events_,_thread-local storage_

### Process

```
HANDLE ProcessCreate(const char *application_uri,
                     
                     const char *manifest_uri,
                     
                     const char **args,uint flags);
```





