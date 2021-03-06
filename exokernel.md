SPACE是一种"submicro-kernel"，仅提供用自陷和体系接口描述的底层核。该系统与EXO很像，但是却没有进一步的记载。
SPIN系统建立了一个微内核系统，允许应用程序自主的决定策略然后安全的将扩展下载到内核中，EXO比该系统层次更低，赋予应用的权限更多。
Cache-Kernel提供底层核心，支持多个应用级的操作系统。主要着眼于灵活性，而不是安全的将硬件资源暴露给应用程序。
Nemesis与EXo具有很多相似之处，不同的是设计目标具有很大差异。Nemesis的设计目标是改善多媒体应用的服务质量。

如果再次获得资源语义？
统一通过代码下载方式允许不受信的软件向元核传递语义。对网络应用，采用包过滤器，对磁盘，采用确定元数据解释器。
元核采用上传代码的方式避免过多的状态保护，也就无需知道资源的语义。

如何保护共享状态？
递归的利用元核准则：将库划分为特权和非特权两部分，特权库包含所有保护代码，被所有使用该状态的应用所使用。非特权库包含管理代码，可以被替换。让应用使用特权库可以采用三种方法：在服务器中替换，使用限制语言和可信编译嚣，下载代码到核心。

如何在不增加负载的情况下进行资源保护？
让应用跟踪所有权是否可信？

###设计原则
资源保护一般包含三个任务：1.跟踪资源的所有权；2.通过守护资源使用情况或者绑定点来保护资源；3.取消资源访问权。
将管理与保护分离
暴露硬件资源
暴露资源分配
暴露废除机制
保护细粒度单元
暴露命名
暴露信息

###内核对保护抽象的支持
传统操作系统中，对资源的保护是因为他们本身就是高层抽象。例如文件，包括元数据，磁盘块，缓冲区缓存页等，上述所有都被高层文件对象的访问权限进行守护。而外核允许高层资源直接的访问底层资源，外核系统必须提供类似UNIX的保护，包括高层对象的访问控制。设计的一个主要挑战就是找到一种核接口来允许来自上层的访问控制而不需要修改其中的特定实现或者组织应用控制硬件资源。
为了应对该挑战，我们在内核中设计了保护机制，同时让应用下载代码来增强该机制。对前一种方法，外核提供一种软件抽象从而将硬件资源绑定在一起。例如缓冲区缓存寄存器与缓存他们的内存页绑定在一起。应用可以控制物理页和磁盘IO，也可以安全的使用彼此的缓存页。外核保护极值保证一个进程只可以访问一个缓存页，前提是进程拥有对应磁盘块相同的访问级别。
一般而言，为了让应用程序下载代码，外核给予他们一种封装抽象状态的机制，从而保证其不发生变化。这种策略对于硬件抽象的必要性来源于硬件抽象与保护无法对应起来。例如，文件会在更正时间内要求合法更新。最古老的代码下载方式是包过滤。包过滤是是应用中写好的代码片段，令应用可以下载到核中并选择所需要的网络数据包。
  但是，当这些软件抽象进驻到核中后，她们会在可信用户层服务器中实现。微内核管理方式会带来额外的上下文切换开销。此外，在用户层划分功能更为复杂。
  从另一个角度来看，代码下载提供了了一种跨越用户信任边界的语义推送方式。这对于外核心系统而言更为重要。通过将系统代码移入库中，外核也一走了理解资源语义的代码，因此丧失了保护资源的功能。
  共享抽象层次：
  互信任。单向信任。互不信任。
  As an example, consider the problem of writing cached disk blocks to stable storage in a way that guarantees
consistency across reboots. Rather than an exokernel deciding on a particular write ordering and having to struggle
with the associated tradeoffs in scheduling heuristics and caching decisions required, it can instead allow the application
to construct schedules, retaining for the much simpliﬁed task of merely checking that any application schedule gives
appropriate consistency guarantees. 
Because libOSes understand the higher-level semantics of their abstractions, they “just know” many things that an
exokernel does not. For example, that related ﬁles will likely be clustered together and if one block is fetched, the
succeeding eight blocks should be as well. Thus, a variant of the above methodology is designing interfaces where
actions do not require justiﬁcation. As an example, consider the act of fetching a disk block in core. If a ﬁle system
must present credentials before the kernel will allow the fetch to be initiated, then it faces serious problems doing
the prefetching it needs, since it would ﬁrst have to read in all ﬁle directory entries, show each ﬁle's capability to the
kernel, and only then initiate the fetches. In contrast, by only performing access control when the actual data in the
block or read or written, rather then when the block is fetched, these disk reads can be initiated all at once.
