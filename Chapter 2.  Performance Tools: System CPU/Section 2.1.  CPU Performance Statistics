### 2.1\. CPU Performance Statistics

Each system-wide Linux performance tool provides different ways to extract similar statistics. Although no tool displays all the statistics, some of the tools display the same statistics. Rather than describe the meaning of the statistics multiple times (once for each tool), we review them once before all the tools are described.

<a name="ch02lev2sec1"></a>

#### 2.1.1\. Run Queue Statistics

In Linux, a process can be either runnable <a name="iddle0056"></a><a name="iddle0057"></a>or blocked waiting for an event to complete. A blocked process may be waiting for data from an I/O device or the results of a system call. If a process is runnable, that means that it is competing for the CPU time with the other processes that are also runnable. A runnable process is not necessarily using the CPU, but when the Linux scheduler is deciding which process to run next, it picks from the list of runnable processes. When these processes are runnable, but waiting to use the processor, they form a line called the run queue. The longer the run queue, the more processes wait in line.

The performance tools commonly show the number of processes that are runnable and the number of processes that are blocked waiting for <a name="iddle0058"></a><a name="iddle0059"></a>I/O. Another <a name="iddle0060"></a>common system statistic is that of load average. The load on a system is the total amount of running and runnable process. For example, if two processes were running and three were available to run, the system's load would be five. The load average is the amount of load over a given amount of time. Typically, the load average is taken over 1 minute, 5 minutes, and 15 minutes. This enables you to see how the load changes over <a name="iddle0061"></a>time.

<a name="ch02lev2sec2"></a>

#### 2.1.2\. Context Switches

Most modern processors can <a name="iddle0062"></a>run only one process or thread at a time. Although some processors, such hyperthreaded processors, can actually run more than one process simultaneously, Linux treats them as multiple single-threaded processors. To create the illusion that a given single processor runs multiple tasks simultaneously, the Linux kernel constantly switches between different processes. The switch between different processes is called a context switch, because when it happens, the CPU saves all the context information from the old process and retrieves all the context information for the new process. The context contains a large amount of information that Linux tracks for each process, including, among others, which instruction the process is executing, which memory it has allocated, and which files the process has open. Switching these contexts can involve moving a large amount of information, and a context switch can be quite expensive. It is a good idea to minimize the number of context switches if possible.

To avoid context switches, it is important to know how they can happen. First, context switches can result from <a name="iddle0063"></a>kernel scheduling. To guarantee that each process receives a fair share of processor time, the kernel periodically interrupts the running process and, if appropriate, the kernel scheduler decides to start another process rather than let the current process continue executing. It is possible that your system will context switch every time this periodic interrupt or timer occurs. The number of timer interrupts per second varies per architecture and kernel version. One easy way to check how often the interrupt fires is to use the <tt>/proc/interrupts</tt> file to determine the number of interrupts that have occurred over a known amount of time. This <a name="iddle0064"></a>is demonstrated in [Listing 2.1](ch02lev1sec1.html#ch02ex01).

<a name="ch02ex01"></a>

##### Listing 2.1\.

<pre>root@localhost asm-i386]# cat /proc/interrupts | grep timer

; sleep 10 ; cat /proc/interrupts | grep timer

  0:   24060043          XT-PIC  timer

  0:   24070093          XT-PIC  timer

</pre>

In <a name="iddle0065"></a>[Listing 2.1](ch02lev1sec1.html#ch02ex01), we ask the kernel to show us how many times the timer has fired, wait 10 seconds, and then ask again. That means that on this machine, the timer fires at a rate of (24,070,093 – 24,060,043) interrupts / (10 seconds) or ~1,000 interrupts/sec. If you have significantly more context switches than timer interrupts, the context switches are most likely caused by an I/O request or some other long-running system call (such as a sleep). When an application requests an operation that can not complete immediately, the kernel starts the operation, saves the requesting process, and tries to switch to another process if one is ready. This allows the processor to keep busy if <a name="iddle0066"></a>possible.

<a name="ch02lev2sec3"></a>

#### 2.1.3\. Interrupts

In <a name="iddle0067"></a><a name="iddle0068"></a>addition, periodically, the processor receives an interrupt by hardware devices. These interrupts are usually triggered by a device that has an event that needs to be handled by the kernel. For example, if a disk controller has just finished retrieving a block from the drive and is ready for the kernel to use it, the disk controller may trigger an interrupt. For each interrupt the kernel receives, an interrupt handler is run if it has been registered for that interrupt; otherwise, the interrupt is ignored. These interrupt handlers run at a very high priority in the system and typically execute very quickly. Sometimes, the interrupt handler has work that needs to be done, but does not require the high priority, so it launches a "bottom half," which is also known as a soft-interrupt handler. If there are a high number of interrupts, the kernel can spend a large amount of time servicing these interrupts. The file <tt>/proc/interrupts</tt><a name="iddle0069"></a> can be examined to show which interrupts are firing on which <a name="iddle0070"></a><a name="iddle0071"></a>CPUs.

<a name="ch02lev2sec4"></a>

#### 2.1.4\. CPU Utilization

CPU utilization <a name="iddle0072"></a>is a straightforward concept. At any given time, the CPU can be doing one of seven things. First, it can be idle, which means that the processor is not actually doing any work and is waiting for something to do. Second, the CPU can be running user code, which is specified as "user" time. Third, the CPU can be executing code in the Linux kernel on behalf of the application code. This is "system" time. Fourth, the CPU can be executing user code that has been "nice"ed or set to run at a lower priority than normal processes. Fifth, the CPU can be in <tt>iowait</tt>, which mean the system is spending its time waiting for I/O (such as disk or network) to complete. Sixth, the CPU can be in <tt>irq</tt> state, which means it is in high-priority kernel code handling a hardware interrupt. Finally, the CPU can be in <tt>softirq</tt> mode, which means it is executing kernel code that was also triggered by an interrupt, but it is running at a lower priority (the bottom-half code). This can happen when a device interrupt occurs, but the kernel needs to do some work with it before it is ready to hand it over to user space (for example, with a network packet).

Most performance tools specify these values as a percentage of the total CPU time. These times can range from 0 percent to 100 percent, but all three total 100 percent. A system with a high "system" percentage is spending most of its time in the kernel. Tools such as <tt>oprofile</tt> can help determine where this time is being spent. A system that has a high "user" time spends most of its time running applications. The next chapter shows how to use performance tools to track down problems in these cases. If a system is spending most of its time <tt>iowait</tt> when it should be doing work, it is most likely waiting for I/O from a device. It may be a disk, network card, or something else causing the <a name="iddle0073"></a>slowdown.