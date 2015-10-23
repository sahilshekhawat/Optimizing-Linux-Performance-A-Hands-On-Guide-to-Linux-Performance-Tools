### 9.4\. Optimizing a System

Sometimes, it is important to approach a misbehaving system and figure out exactly what is slowing everything down.

Because we are investigating a system-wide problem, the cause can be anywhere from user applications to system libraries to the Linux kernel. Fortunately, with Linux, unlike many other operating systems, you can get the source for most if not all applications on the system. If necessary, you can fix the problem and submit the fix to the maintainers of that particular piece. In the worst case, you can run a fixed version locally. This is the power of open-source software.

[Figure 9-2](ch09lev1sec4.html#ch09fig02) shows a flowchart of how we will diagnose a system-wide performance <a name="iddle2179"></a><a name="iddle2180"></a>problem.

<a name="ch09fig02"></a>

<center>

##### Figure 9-2\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig02_alt.gif)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig02_alt.gif)

[Go to](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig02_alt.gif) [Section 9.4.1](ch09lev1sec4.html#ch09lev2sec7) to begin the investigation.

<a name="ch09lev2sec7"></a>

#### 9.4.1\. Is the System CPU-Bound?

Use <tt>top</tt>, <tt>procinfo</tt>, or <tt>mpstat</tt> and determine <a name="iddle2181"></a><a name="iddle2182"></a><a name="iddle2183"></a>where the system is spending its time. If the entire system is spending less than 5 percent of the total time in idle and wait modes, your system is CPU-bound. Proceed to [Section 9.4.3](ch09lev1sec4.html#ch09lev2sec9). Otherwise, proceed to [Section 9.4.2](ch09lev1sec4.html#ch09lev2sec8).

<a name="ch09lev2sec8"></a>

#### 9.4.2\. Is a Single Processor CPU-Bound?

Although the <a name="iddle2184"></a><a name="iddle2185"></a><a name="iddle2186"></a>system as a whole may not be CPU-bound, in a symmetric multiprocessing (SMP) or hyperthreaded system, an individual processor may be CPU-bound.

Use <tt>top</tt> or <tt>mpstat</tt> to determine whether an individual CPU has less than 5 percent in idle and wait modes. If it does, one or more CPU is CPU-bound; in this case, go to [Section 9.4.4](ch09lev1sec4.html#ch09lev2sec10).

Otherwise, nothing is CPU-bound. Go to [Section 9.4.7](ch09lev1sec4.html#ch09lev2sec13).

<a name="ch09lev2sec9"></a>

#### 9.4.3\. Are One or More Processes Using Most of the System CPU?

The next <a name="iddle2187"></a><a name="iddle2188"></a><a name="iddle2189"></a>step is to figure out whether any particular application or group of applications is using the CPU. The easiest way to do this is to run <tt>top</tt>. By default, <tt>top</tt> sorts the processes that use the CPU in descending order. <tt>top</tt> reports CPU usage for a process as the sum of the user and system time spent on behalf of that process. For example, if an application spends 20 percent of the CPU in user space code, and 30 percent of the CPU in system code, <tt>top</tt> will report that the process has consumed 50 percent of the CPU. Sum up the CPU time of all the processes. If that time is significantly less than the system-wide system plus user time, the kernel is doing significant work that is <span class="docEmphasis">not</span> on the behalf of applications. Go to [Section 9.4.5](ch09lev1sec4.html#ch09lev2sec11).

Otherwise, go to [Section 9.5.1](ch09lev1sec5.html#ch09lev2sec17) once for each process to determine <a name="iddle2190"></a><a name="iddle2191"></a><a name="iddle2192"></a>where it is spending its time.

<a name="ch09lev2sec10"></a>

#### 9.4.4\. Are One or More Processes Using Most of an Individual CPU?

The next step is to <a name="iddle2193"></a><a name="iddle2194"></a><a name="iddle2195"></a>figure out whether any particular application or group of applications is using the individual CPUs. The easiest way to do this is to run <tt>top</tt>. By default, <tt>top</tt> sorts the processes that use the CPU in descending order. When reporting CPU usage for a process, <tt>top</tt> shows the total CPU and system time that the application uses. For example, if an application spends 20 percent of the CPU in user space code, and 30 percent of the CPU in system code, <tt>top</tt> will report that the application has consumed 50 percent of the CPU.

First, run <tt>top</tt>, and then add the last CPU to the fields that <tt>top</tt> displays. Turn on Irix mode so that <tt>top</tt> shows the amount of CPU time used per processor rather than the total system. For each processor that has a high utilization, sum up the CPU time of the application or applications running on it. If the sum of the application time is less than 75 percent of the sum of the kernel plus user time for that CPU, it appears as the kernel is spending a significant amount of time on something other than the applications; in this case, go to [Section 9.4.5](ch09lev1sec4.html#ch09lev2sec11). Otherwise, the applications are likely to be the cause of the CPU usage; for each application, go to <a name="iddle2196"></a><a name="iddle2197"></a><a name="iddle2198"></a>[Section 9.5.1](ch09lev1sec5.html#ch09lev2sec17).

<a name="ch09lev2sec11"></a>

#### 9.4.5\. Is the Kernel Servicing Many Interrupts?

It appears as <a name="iddle2199"></a><a name="iddle2200"></a>if the kernel is spending a lot of time doing work not on behalf of an application. One explanation for this is an I/O card that is raising many interrupts, such as a busy network card. Run <tt>procinfo</tt> or <tt>cat /proc/interrupts</tt> to determine how many interrupts are being fired, how often they are being fired, and which devices are causing them. This may provide a hint as to what the system is doing. Record this information and proceed to [Section 9.4.6](ch09lev1sec4.html#ch09lev2sec12).

<a name="ch09lev2sec12"></a>

#### 9.4.6\. Where Is Time Spent in the Kernel?

Finally, we will find <a name="iddle2201"></a><a name="iddle2202"></a><a name="iddle2203"></a>out exactly what the kernel is doing. Run <tt>oprofile</tt> on the system and record which kernel functions consume a significant amount of time (greater than 10 percent of the total time). Try reading the kernel source for those functions or searching the Web for references to those functions. It might not be immediately clear what exactly those functions do, but try to figure out what kernel subsystem the functions are in. Just determining which subsystem is being used (such as memory, network, scheduling, or disk) might be enough to determine what is going wrong.

It also might be possible to figure out why these functions are called based on what they are doing. If the functions are device specific, try to figure out why the particular device is being used (especially if it also has a high number of interrupts). E-mail others who may have seen similar problems, and possibly contact kernel developers.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec13"></a>

#### 9.4.7\. Is the Amount of Swap Space Being Used Increasing?

The next <a name="iddle2204"></a><a name="iddle2205"></a><a name="iddle2206"></a><a name="iddle2207"></a>step is the check whether the amount of swap space being used is increasing. Many of the system-wide performance tools such as <tt>top</tt>, <tt>vmstat</tt>, <tt>procinfo</tt>, and <tt>gnome-system-info</tt> provide this information. If the amount of swap is increasing, you need to figure out what part of the system is using more memory. To do this, go to [Section 9.6.1](ch09lev1sec6.html#ch09lev2sec22).

If the amount of used swap is not increasing, go to [Section 9.4.8](ch09lev1sec4.html#ch09lev2sec14).

<a name="ch09lev2sec14"></a>

#### 9.4.8\. Is the System I/O-Bound?

While <a name="iddle2208"></a><a name="iddle2209"></a><a name="iddle2210"></a>running <tt>top</tt>, check to <tt>see</tt> whether the system is spending a high percentage of time in the wait state. If this is greater than 50 percent, the system is spending a large amount of time waiting for I/O, and we have to determine what type of I/O this is. Go to [Section 9.4.9](ch09lev1sec4.html#ch09lev2sec15).

If the system is not spending a large amount of time waiting for I/O, you have reached a problem not covered in this book. Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec15"></a>

#### 9.4.9\. Is the System Using Disk I/O?

Next, run <tt>vmstat</tt> (or <tt>iostat</tt>) and see how <a name="iddle2211"></a><a name="iddle2212"></a><a name="iddle2213"></a>many blocks are being written to and from the disk. If a large number of blocks are being written to and read from the disk, this may be a disk bottleneck. Go to [Section 9.7.1](ch09lev1sec7.html#ch09lev2sec32). Otherwise, continue to [Section 9.4.10](ch09lev1sec4.html#ch09lev2sec16).

<a name="ch09lev2sec16"></a>

#### 9.4.10\. Is the System Using Network I/O?

Next, we see <a name="iddle2214"></a><a name="iddle2215"></a><a name="iddle2216"></a>whether the system is using a significant amount of network I/O. It is easiest to run <tt>iptraf</tt>, <tt>ifconfig</tt>, or <tt>sar</tt> and see how much data is being transferred on each network device. If the network traffic is near the capacity of the network device, this may be a network bottleneck. Go to [Section 9.8.1](ch09lev1sec8.html#ch09lev2sec35). If none of the network devices seem to be passing network traffic, the kernel is waiting on some other I/O device that is not covered in this book. It may be useful to see what functions the kernel is calling and what devices are interrupting the kernel. Go to [Section 9.4.5](ch09lev1sec4.html#ch09lev2sec11).