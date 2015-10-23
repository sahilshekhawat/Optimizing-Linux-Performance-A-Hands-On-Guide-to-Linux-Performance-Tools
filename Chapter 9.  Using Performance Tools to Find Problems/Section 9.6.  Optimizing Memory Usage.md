### 9.6\. Optimizing Memory Usage

Often, it is common that a program that uses a large amount of memory can cause other performance problems to occur, such as cache misses, translation lookaside buffer (TLB) misses, and swapping.

[Figure 9-4](ch09lev1sec6.html#ch09fig04) shows the flowchart of decisions that we will make to figure out how the system memory is being used.

<a name="ch09fig04"></a>

<center>

##### Figure 9-4\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig04_alt.gif)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig04_alt.gif)

[Go to](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig04_alt.gif) [Section 9.6.1](ch09lev1sec6.html#ch09lev2sec22) to start the investigation.

<a name="ch09lev2sec22"></a>

#### 9.6.1\. Is the Kernel Memory Usage Increasing?

To track down <a name="iddle2256"></a><a name="iddle2257"></a><a name="iddle2258"></a><a name="iddle2259"></a>what is using the system's memory, you first have to determine whether the kernel itself is allocating memory. Run <tt>slabtop</tt> and see whether the total size of the kernel's memory is increasing. If it is increasing, jump to [Section 9.6.2](ch09lev1sec6.html#ch09lev2sec23).

If the kernel's memory usage is not increasing, it may be a particular process causing the increase. To track down which process is responsible for the increase in memory usage, go to [Section 9.6.3](ch09lev1sec6.html#ch09lev2sec24).

<a name="ch09lev2sec23"></a>

#### 9.6.2\. What Type of Memory Is the Kernel Using?

If the kernel's <a name="iddle2260"></a><a name="iddle2261"></a><a name="iddle2262"></a><a name="iddle2263"></a><a name="iddle2264"></a>memory usage is increasing, once again run <tt>slabtop</tt> to determine what type of memory the kernel is allocating. The name of the slab can give some indication about why that memory is being allocated. You can find more details on each slab name in the kernel source and through Web searches. By just searching the kernel source for the name of that slab and determining which files it is used in, it may become clear why it is allocated. After you determine which subsystem is allocating all that memory, try to tune the amount of maximum memory that the particular subsystem can consume, or reduce the usage of that subsystem.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec24"></a>

#### 9.6.3\. Is a Particular Process's Resident Set Size Increasing?

Next, you <a name="iddle2265"></a>can use <tt>top</tt> or <tt>ps</tt> to see whether a particular process's resident set size is increasing. It is easiest to add the <tt>rss</tt> field to the output of <tt>top</tt> and sort by memory usage. If a particular process is increasingly using more memory, we need to figure out what type of memory it is using. To figure out what type of memory the application is using, go to [Section 9.6.6](ch09lev1sec6.html#ch09lev2sec27). If no particular process is using more memory, go to [Section 9.6.4](ch09lev1sec6.html#ch09lev2sec25).

<a name="ch09lev2sec25"></a>

#### 9.6.4\. Is Shared Memory Usage Increasing?

Use <tt>ipcs</tt> to determine whether the amount of shared memory being used is increasing. If it is, go to [Section 9.6.5](ch09lev1sec6.html#ch09lev2sec26) to determine which processes are using the memory. Otherwise, you have a system memory leak not covered in this book. Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec26"></a>

#### 9.6.5\. Which Processes Are Using the Shared Memory?

Use <tt>ipcs</tt> to determine <a name="iddle2266"></a>which processes are using and allocating the shared memory. After the processes that use the shared memory have been identified, investigate the individual processes to determine why the memory is being using for each. For example, look in the application's source code for calls to <tt>shmget</tt> (to allocate shared memory) or <tt>shmat</tt> (to attach to it). Read the application's documentation and look for options that explain and can reduce the application's use of shared memory.

Try to reduce shared memory usage and go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec27"></a>

#### 9.6.6\. What Type of Memory Is the Process Using?

The easiest way to see <a name="iddle2267"></a>what types of memory the process is using is to look at its status in the <tt>/proc</tt> file system. This file, <tt>cat /proc/<pid>/status</tt>, gives a breakdown of the processs memory usage.

If the process has a large and increasing <tt>VmStk</tt>, this means that the processs stack size is increasing. To analyze why, go to [Section 9.6.7](ch09lev1sec6.html#ch09lev2sec28).

If the process has a large <tt>VmExe</tt>, that means that the executable size is big. To figure out which functions in the executable contribute to this size, go to [Section 9.6.8](ch09lev1sec6.html#ch09lev2sec29). If the process has a large <tt>VmLib</tt>, that means that the process is using either a large number of shared libraries or a few large-sized shared libraries. To figure out which libraries contribute to this size, go to [Section 9.6.9](ch09lev1sec6.html#ch09lev2sec30). If the process has a large and increasing <tt>VmData</tt>, this means that the processs data area, or heap, is increasing. To analyze why, go to <a name="iddle2268"></a>[Section 9.6.10](ch09lev1sec6.html#ch09lev2sec31).

<a name="ch09lev2sec28"></a>

#### 9.6.7\. What Functions Are Using All of the Stack?

To figure out <a name="iddle2269"></a><a name="iddle2270"></a>which functions are allocating large amounts of stack, we have to use <tt>gdb</tt> and a little bit of trickery. First, attach to the running process using <tt>gdb</tt>. Then, ask <tt>gdb</tt> for a backtrace using <tt>bt</tt>. Next, print out the stack pointer using <tt>info registers esp</tt> (on i386). This prints out the current value of the stack pointer. Now type <tt>up</tt> and print out the stack pointer. The difference (in hex) between the previous stack pointer and the current stack pointer is the amount of stack that the previous function is using. Continue this up the backtrace, and you will be able to see which function is using most of the stack.

When you figure out which function is consuming most of the stack, or whether it is a combination of functions, you can modify the application to reduce the size and number of calls to this function (or these functions). Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec29"></a>

#### 9.6.8\. What Functions Have the Biggest Text Size?

If the executable <a name="iddle2271"></a><a name="iddle2272"></a>has a sizable amount of memory being used, it may be useful to determine which functions are taking up the greatest amount of space and prune unnecessary functionality. For an executable or library compiled with symbols, it is possible to ask <tt>nm</tt> to show the size of all the symbols and sort them with the following command:

<pre>nm -S –size-sort

</pre>

With the knowledge of the size of each function, it may be possible to reduce their size or remove unnecessary code from the <a name="iddle2273"></a><a name="iddle2274"></a>application.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec30"></a>

#### 9.6.9\. How Big Are the Libraries That the Process Uses?

The easiest way <a name="iddle2275"></a><a name="iddle2276"></a><a name="iddle2277"></a>to see which libraries a process is using and their individual sizes is to look at the processs map in the <tt>/proc</tt> file system. This file, <tt>cat /proc/<pid>/map</tt>, will shows each of the libraries and the size of their code and data. When you know which libraries a process is using, it may be possible to eliminate the usage of large libraries or use alternative and smaller libraries. However, you must be careful, because removing large libraries may not reduce overall system memory usage.

If any other applications are using the library, which you can determine by running <tt>lsof</tt> on the library, the libraries will already be loaded into memory. Any new applications that use it do not require an additional copy of the library to be loaded into memory. Switching your application to use a different library (even if it is smaller) actually increases total memory usage. This new library will not be used by any other processes and will require new memory to be allocated. The best solution may be to shrink the size of the libraries themselves or modify them so that they use less memory to store library-specific data. If this is possible, all applications will benefit.

To find the size of the functions in a particular library, go to [Section 9.6.8](ch09lev1sec6.html#ch09lev2sec29); otherwise, go to <a name="iddle2278"></a><a name="iddle2279"></a><a name="iddle2280"></a>[Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec31"></a>

#### 9.6.10\. What Functions Are Allocating Heap Memory?

If your application is <a name="iddle2281"></a><a name="iddle2282"></a><a name="iddle2283"></a>written in C or C++, you can figure out which functions are allocating heap memory by using the memory profiler <tt>memprof</tt>. <tt>memprof</tt> can dynamically show how memory usage grows as the application is used.

If your application is written in Java, add the <tt>-Xrunhprof</tt> command-line parameter to the <tt>java</tt> command line; it gives details about how the application is allocating memory. If your application is written in C# (Mono), add the <tt>-profile</tt> command-line parameter to the <tt>mono</tt> command line, and it gives details about how the application is allocating memory.

After you know which functions allocate the largest amounts of memory, it may be possible to reduce the size of memory that is allocated. Programmers often overallocate memory just to be on the safe side because memory is cheap and out-of-bounds errors are hard to detect. However, if a particular allocation is causing memory problems, careful analysis of the minimum allocation makes it possible to significantly reduce memory usage and still be <a name="iddle2284"></a><a name="iddle2285"></a><a name="iddle2286"></a>safe. Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).