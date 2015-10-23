### 9.5\. Optimizing Process CPU Usage

When a particular process or application has been determined to be a CPU bottleneck, it is necessary to determine where (and why) it is spending its time.

[Figure 9-3](ch09lev1sec5.html#ch09fig03) shows the method for investigating a processs CPU usage.

<a name="ch09fig03"></a>

<center>

##### Figure 9-3\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig03_alt.gif)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig03_alt.gif)

[Go to](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig03_alt.gif) [Section 9.5.1](ch09lev1sec5.html#ch09lev2sec17) to begin the investigation.

<a name="ch09lev2sec17"></a>

#### 9.5.1\. Is the Process Spending Time in User or Kernel Space?

You can use the <a name="iddle2217"></a><a name="iddle2218"></a><a name="iddle2219"></a><a name="iddle2220"></a><a name="iddle2221"></a><a name="iddle2222"></a><a name="iddle2223"></a><a name="iddle2224"></a><a name="iddle2225"></a><a name="iddle2226"></a><tt>time</tt> command to determine whether an application is spending its time in kernel or user mode. <tt>oprofile</tt> can also be used to determine where time is spent. By profiling per process, it is possible to see whether a process is spending its time in the kernel or user space.

If the application is spending a significant amount of time in kernel space (greater than 25 percent), go to [Section 9.5.2](ch09lev1sec5.html#ch09lev2sec18). Otherwise, go to [Section 9.5.3](ch09lev1sec5.html#ch09lev2sec19).

<a name="ch09lev2sec18"></a>

#### 9.5.2\. Which System Calls Is the Process Making, and How Long Do They Take to Complete?

Next, run <tt>strace</tt> to see <a name="iddle2227"></a><a name="iddle2228"></a><a name="iddle2229"></a><a name="iddle2230"></a><a name="iddle2231"></a><a name="iddle2232"></a>which system calls are made and how long they take to complete. You can also run <tt>oprofile</tt> to see which kernel functions are being called.

It may be possible to increase performance by minimizing the number of system calls made or by changing which systems calls are made on behalf of the program. Some of the system's calls may be unexpected and a result of the application's calls to various libraries. You can run <tt>ltrace</tt> and <tt>strace</tt> to help determine why they are being made.

Now that the problem has been identified, it is up to you to fix it. Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec19"></a>

#### 9.5.3\. In Which Functions Does the Process Spend Time?

Next, <a name="iddle2233"></a><a name="iddle2234"></a><a name="iddle2235"></a>run <tt>oprofile</tt> on the application using the cycle event to determine which functions are using all the CPU cycles (that is, which functions are spending all the application time).

Keep in mind that although <tt>oprofile</tt> shows you how much time was spent in a process, when profiling at the function level, it is not clear whether a particular function is hot because it is called very often or whether it just takes a long time to complete.

One way to determine which case is true is to acquire a source-level annotation from <tt>oprofile</tt> and look for instructions/source lines that should have little overhead (such as assignments). The number of samples that they have will approximate the number of times that the function was called relative to other high-cost source lines. Again, this is only approximate because <tt>oprofile</tt> samples only the CPU, and out-of-order processors can misattribute some cycles.

It is also helpful to get a call graph of the functions to determine how the hot functions are being called. To do this, go to <a name="iddle2236"></a><a name="iddle2237"></a><a name="iddle2238"></a><a name="iddle2239"></a>[Section 9.5.4](ch09lev1sec5.html#ch09lev2sec20).

<a name="ch09lev2sec20"></a>

#### 9.5.4\. What Is the Call Tree to the Hot Functions?

Next, you <a name="iddle2240"></a><a name="iddle2241"></a><a name="iddle2242"></a><a name="iddle2243"></a><a name="iddle2244"></a>can figure out how and why the time-consuming functions are being called. Running the application with <tt>gprof</tt> can show the call tree for each function. If the time-consuming functions are in a library, you can use <tt>ltrace</tt> to see which functions. Finally, you can use newer versions of <tt>oprofile</tt> that support call-tree tracing. Alternatively, you can run the application in <tt>gdb</tt> and set a breakpoint at the hot function. You can then run that application, and it will break during every call to the hot function. At this point, you can generate a backtrace and see exactly which functions and source lines made the call.

Knowing which functions <a name="iddle2245"></a><a name="iddle2246"></a><a name="iddle2247"></a><a name="iddle2248"></a><a name="iddle2249"></a>call the hot functions may enable you to eliminate or reduce the calls to these functions, and correspondingly speed up the application.

If reducing the calls to the time-consuming functions did not speed up the application, or it is not possible to eliminate these functions, go to [Section 9.5.5](ch09lev1sec5.html#ch09lev2sec21).

Otherwise, go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec21"></a>

#### 9.5.5\. Do Cache Misses Correspond to the Hot Functions or Source Lines?

Next, run <a name="iddle2250"></a><a name="iddle2251"></a><a name="iddle2252"></a><a name="iddle2253"></a><a name="iddle2254"></a><a name="iddle2255"></a><tt>oprofile</tt>, <tt>cachegrind</tt>, and <tt>kcache</tt> against your application to see whether the time-consuming functions or source lines are those with a high number of cache misses. If they are, try to rearrange or compress your data structures and accesses to make them more cache friendly. If the hot lines do not correspond to high cache misses, try to rearrange your algorithm to reduce the number of times that the particular line or function is executed.

In any event, the tools have told you as much as they can, so go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).