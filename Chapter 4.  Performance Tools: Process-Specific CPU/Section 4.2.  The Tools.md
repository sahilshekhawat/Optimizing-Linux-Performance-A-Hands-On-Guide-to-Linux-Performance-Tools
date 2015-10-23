	### 4.2\. The Tools

Linux has a variety of tools to help you determine which pieces of an application are the primary users of the CPU. This section describes these tools.

<a name="ch04lev2sec4"></a>

#### 4.2.1\. time

The <tt>time</tt> command <a name="iddle0786"></a><a name="iddle0787"></a><a name="iddle0788"></a>performs a basic function when testing a command's performance, yet it is often the first place to turn. The <tt>time</tt> command acts as a stopwatch and times how long a command takes to execute. It measures three types of time. First, it measures the real or elapsed time, which is the amount of time between when the program started and finished execution. Next, it measures the user time, which is the amount of time that the CPU spent executing application code on behalf of the program. Finally, <tt>time</tt> measures system time, which is the amount of time the CPU spent executing system or kernel code on behalf of the application.

<a name="ch04lev3sec1"></a>

##### 4.2.1.1 CPU Performance-Related Options

The <tt>time</tt> command (see [Table 4-1](ch04lev1sec2.html#ch04table01)) is invoked in the following manner:

<pre>time [-v] application

</pre>

<a name="ch04table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-1\. <span class="docEmphasis"><tt>time</tt></span> Command-Line Options

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-v</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0789"></a>This option presents a verbose display of the program's time and statistics. Some statistics are zeroed out, but more statistics are valid with Linux kernel v2.6 than with Linux kernel v2.4.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Most of the valid statistics are present in both the standard and verbose mode, but the verbose mode provides a better description for each statistic.<a name="iddle0790"></a><a name="iddle0791"></a><a name="iddle0792"></a>

</td>

</tr>

</tbody>

</table>

The <tt>application</tt> is timed, and information about its CPU usage is displayed on standard output after it has <a name="iddle0793"></a><a name="iddle0794"></a><a name="iddle0795"></a>completed.

[Table 4-2](ch04lev1sec2.html#ch04table02) describes <a name="iddle0796"></a><a name="iddle0797"></a><a name="iddle0798"></a>the valid output statistic that the <tt>time</tt> command provides. The rest are not measured and always display zero.

<a name="ch04table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-2\. CPU-Specific <span class="docEmphasis"><tt>time</tt></span> Output

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

User time (seconds)

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0799"></a>This is the number of seconds of CPU spent by the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

System time (seconds)

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0800"></a>This is the number of seconds spent in the Linux kernel on behalf of the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Elapsed (wall-clock) time (h:mm:ss or m:ss)

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of time elapsed (in wall-clock <a name="iddle0801"></a>time) between when the application was launched and when it completed.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Percent of CPU this job got

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0802"></a>This is the percentage of the CPU that the process consumed as it was running.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Major (requiring I/O) page faults

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0803"></a>The number of major page faults or those that required a page of memory to be read from disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Minor (reclaiming a frame) page faults

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0804"></a>The number of minor page faults or those that could be filled without going to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Swaps

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0805"></a>This is the number of times the process was swapped to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Voluntary context switches

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0806"></a>The number of times the process yielded the CPU (for example, by going to sleep).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Involuntary context switches:

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0807"></a>The number of times the CPU was taken from the process.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Page size (bytes)

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0808"></a>The page size of the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Exit status

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0809"></a>The exit status of the application.

</td>

</tr>

</tbody>

</table>

This command is a good way to start an investigation. It displays how long the application is taking to execute and how much of that time is spent in the Linux kernel versus your <a name="iddle0810"></a><a name="iddle0811"></a><a name="iddle0812"></a>application.

<a name="ch04lev3sec2"></a>

##### 4.2.1.2 Example Usage

The <tt>time</tt> command included <a name="iddle0813"></a><a name="iddle0814"></a><a name="iddle0815"></a>on Linux is a part of the cross-platform GNU tools. The default command output prints a host of statistics about the commands run, even if Linux does not support them. If the statistics are not available, <tt>time</tt> just prints a zero. The following command is a simple invocation of the <tt>time</tt> command. You can see in [Listing 4.1](ch04lev1sec2.html#ch04ex01) that the elapsed time (~3 seconds) is much greater than the sum of the user (0.9 seconds) and system (0.13 seconds) time, because the application spends most of its time waiting for input and little time using the processor.

<a name="ch04ex01"></a>

##### Listing 4.1\.

<pre>[ezolt@wintermute manuscript]$ /usr/bin/time gcalctool

0.91user 0.13system 0:03.37elapsed 30%CPU (0avgtext+0avgdata 0maxresident)k

0inputs+0outputs (2085major+369minor)pagefaults 0swaps

</pre>

[Listing 4.2](ch04lev1sec2.html#ch04ex02) is an example of <tt>time</tt> displaying verbose output. As you can see, this output shows much more than the typical output of <tt>time</tt>. Unfortunately, most of the statistics are zeros, because they are not supported on Linux. For the most part, the information provided in verbose mode is identical to the output provided in standard mode, but the statistics' labels are much more descriptive. In this case, we can see that this process used 15 percent of the CPU when it was running, and spent 1.15 seconds running user code with .12 seconds running kernel code. It accrued 2,087 major page faults, or memory faults that did not require a trip to disk; it accrued 371 page faults that did require a trip to disk. A high number of major faults would indicate that the operating system was constantly going to disk when the application tried to use memory, which most likely means that the kernel was swapping a significant <a name="iddle0816"></a><a name="iddle0817"></a><a name="iddle0818"></a>amount.

<a name="ch04ex02"></a>

##### Listing 4.2\.

<pre>[ezolt@wintermute manuscript]$ /usr/bin/time --verbose gcalctool

        Command being timed: "gcalctool"

        User time (seconds): 1.15

        System time (seconds): 0.12

        Percent of CPU this job got: 15%

        Elapsed (wall clock) time (h:mm:ss or m:ss): 0:08.02

        Average shared text size (kbytes): 0

        Average unshared data size (kbytes): 0

        Average stack size (kbytes): 0

        Average total size (kbytes): 0

        Maximum resident set size (kbytes): 0

        Average resident set size (kbytes): 0

        Major (requiring I/O) page faults: 2087

        Minor (reclaiming a frame) page faults: 371

        Voluntary context switches: 0

        Involuntary context switches: 0

        Swaps: 0

        File system inputs: 0

        File system outputs: 0

        Socket messages sent: 0

        Socket messages received: 0

        Signals delivered: 0

        Page size (bytes): 4096

        Exit status: 0

</pre>

Note that the bash shell <a name="iddle0819"></a>has a built-in <tt>time</tt> command, so if you are running bash and execute <tt>time</tt> without <a name="iddle0820"></a><a name="iddle0821"></a><a name="iddle0822"></a>specifying the path to the executable, you get the following output:

<pre>[ezolt@wintermute manuscript]$ time gcalctool

real  0m3.409s

user  0m0.960s

sys   0m0.090s

</pre>

The bash built-in <tt>time</tt> command can be useful, but it provides a subset of the process execution <a name="iddle0823"></a><a name="iddle0824"></a><a name="iddle0825"></a><a name="iddle0826"></a>information.

<a name="ch04lev2sec5"></a>

#### 4.2.2\. strace

<tt>strace</tt> is a tool that traces <a name="iddle0827"></a><a name="iddle0828"></a><a name="iddle0829"></a>the system calls that a program makes while executing. System calls are function calls made into the Linux kernel by or on behalf of an application. <tt>strace</tt> can show the exact system calls that were made and proves incredibly useful to determine how an application is using the Linux kernel. Tracing down the frequency and length of system calls can be especially valuable when analyzing a large program or one you do not understand completely. By looking at the <tt>strace</tt> output, you can get a feel for how the application is using the kernel and what type of functions it depends on.

<tt>strace</tt> can also be useful when you completely understand an application, but if that application makes calls to system libraries (such as <tt>libc</tt> or <tt>GTK</tt>.) In this case, even though you know where the application makes every system call, the libraries might be making more system calls on behalf of your application. <tt>strace</tt> can quickly show you what calls these libraries are making.

Although <tt>strace</tt> is mainly intended to trace the interaction of processes with the kernel by showing the arguments and results for every system call an application makes, <tt>strace</tt> can also provide summary information that is a little less daunting. After the run of an application, <tt>strace</tt> can provide a table showing the frequency of each system call and the total time spent in calls of that type. This table can be a crucial first piece of information in understanding how your program is <a name="iddle0830"></a><a name="iddle0831"></a><a name="iddle0832"></a>interacting with the Linux kernel.

<a name="ch04lev3sec3"></a>

##### 4.2.2.1 CPU Performance-Related Options

The following <a name="iddle0833"></a><a name="iddle0834"></a><a name="iddle0835"></a>invocation of <tt>strace</tt> is most useful for performance testing:

<pre>strace [-c] [-p pid] [-o file] [--help] [ command [ arg ... ]]

</pre>

If <tt>strace</tt> is run without any options, it displays all the system calls made by the given command on standard error. This can be helpful when trying to figure out why an application is spending a large amount of time in the kernel. [Table 4-3](ch04lev1sec2.html#ch04table03) describes a few <tt>strace</tt> options that are also helpful when tracing a performance problem.

<a name="ch04table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-3\. <span class="docEmphasis"><tt>strace</tt></span> Command-Line Options

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-c</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0836"></a>This causes <tt>strace</tt> to print out a summary of statistics rather than an individual list of all the system calls that are made.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p pid</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0837"></a>This attaches to the process with the given PID and starts tracing.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-o file</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0838"></a>The output of <tt>strace</tt> will be saved in <tt>file</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--help</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0839"></a>Lists a complete summary of the <tt>strace</tt> options

</td>

</tr>

</tbody>

</table>

[Table 4-4](ch04lev1sec2.html#ch04table04) explains the statistics present in output of the <tt>strace</tt> summary option. Each line of output describes a set of statistics for a particular system <a name="iddle0840"></a><a name="iddle0841"></a><a name="iddle0842"></a>call.

<a name="ch04table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-4\. CPU-Specific <span class="docEmphasis"><tt>strace</tt></span> Output

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0843"></a><a name="iddle0844"></a><a name="iddle0845"></a>Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>% time</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0846"></a>Of the total time spent making system calls, this is the percentage of time spent on this one.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>seconds</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0847"></a>This the total number of seconds spent in this system call.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>usecs/call</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0848"></a>This is the number of microseconds spent per system call of this type.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>calls</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0849"></a>This is the total number of calls of this type.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>errors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0850"></a>This is the number of times that this system call returned an error.

</td>

</tr>

</tbody>

</table>

Although the options just described are most relevant to a performance investigation, <tt>strace</tt> can also filter the types of system calls that it traces. The options to select the system calls to trace are described in detail with the <tt>--help</tt> option and in the <tt>strace</tt> man page. For general performance tuning, it is usually not necessary to use them; if needed, however, they <a name="iddle0851"></a><a name="iddle0852"></a><a name="iddle0853"></a>exist.

<a name="ch04lev3sec4"></a>

##### 4.2.2.2 Example Usage

[Listing 4.3](ch04lev1sec2.html#ch04ex03) is an <a name="iddle0854"></a><a name="iddle0855"></a><a name="iddle0856"></a>example of using <tt>strace</tt> to gather statistics about which system calls an application is making. As you can see, <tt>strace</tt> provides a nice profile of the system's calls made on behalf of an application, which, in this case, is <tt>oowriter</tt>. In this example, we look at how <tt>oowriter</tt> is using the read system call. We can see that read is taking the 20 percent of the time by consuming a total of 0.44 seconds. It is called 2,427 times and, on average, each call takes 184 microseconds. Of those calls, 26 return an error.

<a name="ch04ex03"></a>

##### Listing 4.3\.

<pre>[ezolt@wintermute tmp]$ strace -c oowriter

execve("/usr/bin/oowriter", ["oowriter"], [/* 35 vars */]) = 0

Starting OpenOffice.org ...

% time     seconds  usecs/call     calls    errors syscall

------ ----------- ----------- --------- --------- ----------------

 20.57    0.445636         184	    2427	26 read

 18.25    0.395386	   229      1727	   write

 11.69    0.253217	   338       750       514 access

 10.81    0.234119	 16723	      14	 6 waitpid

  9.53    0.206461	  1043       198	   select

  4.73    0.102520	   201       511	55 stat64

  4.58    0.099290	   154       646	   gettimeofday

  4.41    0.095495	    58      1656	15 lstat64

  2.51    0.054279	   277       196	   munmap

  2.32    0.050333	   123       408	   close

  2.07    0.044863	    66	     681       297 open

  1.98    0.042879	   997	      43	   writev

  1.18    0.025614	    12      2107	   lseek

  0.95    0.020563	  1210        17	   unlink

  0.67    0.014550	   231        63	   getdents64

  0.58    0.012656          44       286	   mmap2

  0.53    0.011399          68       167         2 ioctl

  0.50    0.010776         203        53           readv

  0.44    0.009500        2375         4	 3 mkdir

  0.33    0.007233	   603        12           clone

  0.29    0.006255          28       224	   old_mmap

  0.24    0.005240        2620         2	   vfork

  0.24    0.005173          50       104	   rt_sigprocmask

  0.11    0.002311           8       295	   fstat64

</pre>

<tt>strace</tt> does a good job of tracking a process, but it does introduce some overhead when it is running on an application. As a result, the number of calls that <tt>strace</tt> reports is probably more reliable than the amount of time that it reports for each call. Use the times provided by <tt>strace</tt> as a starting point for investigation rather than a highly accurate measurement of how much time was spent in each <a name="iddle0857"></a><a name="iddle0858"></a><a name="iddle0859"></a>call.

<a name="ch04lev2sec6"></a>

#### 4.2.3\. ltrace

<tt>ltrace</tt> is similar <a name="iddle0860"></a><a name="iddle0861"></a><a name="iddle0862"></a><a name="iddle0863"></a><a name="iddle0864"></a>in concept to <tt>strace</tt>, but it traces the calls that an application makes to libraries rather than to the kernel. Although it is primarily used to provide an exact trace of the arguments and return values of library calls, you can also use <tt>ltrace</tt> to summarize how much time was spent in each call. This enables you to figure out both what library calls the application is making and how long each is taking.

Be careful when using <tt>ltrace</tt> because it can generate misleading results. The time spent may be counted twice if one library function calls another. For example, if library function foo() calls function bar(), the time reported for function foo() will be all the time spent running the code in function foo() plus all the time spent in function bar().

With this caveat in mind, it still is a useful tool to figure out how an application is <a name="iddle0865"></a><a name="iddle0866"></a><a name="iddle0867"></a><a name="iddle0868"></a><a name="iddle0869"></a>behaving.

<a name="ch04lev3sec5"></a>

##### 4.2.3.1 CPU Performance-Related Options

<tt>ltrace</tt> provides similar functionality to <tt>strace</tt> and is invoked in a similar way:

<pre>ltrace [-c] [-p pid] [-o filename] [-S] [--help] command

</pre>

In the preceding invocation, <tt>command</tt> is the <tt>command</tt> that you want <tt>ltrace</tt> to trace. Without any options to <tt>ltrace</tt>, it displays all the library calls to standard error. [Table 4-5](ch04lev1sec2.html#ch04table05) describes the ltrace options that are most relevant to a performance investigation.

<a name="ch04table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-5\. <span class="docEmphasis"><tt>ltrace</tt></span> Command-Line Options

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0870"></a><a name="iddle0871"></a><a name="iddle0872"></a><a name="iddle0873"></a><a name="iddle0874"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-c</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0875"></a>This option causes <tt>ltrace</tt> to print a summary of all the calls after the command has completed.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-S</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0876"></a><tt>ltrace</tt> TRaces system calls in addition to library calls, which is identical to the functionality <tt>strace</tt> provides.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p pid</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0877"></a>This traces the process with the given PID.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-o file</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0878"></a>The output of <tt>strace</tt> is saved in <tt>file</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--help</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0879"></a>Displays help information about <tt>ltrace</tt>.

</td>

</tr>

</tbody>

</table>

<a name="iddle0880"></a><a name="iddle0881"></a><a name="iddle0882"></a><a name="iddle0883"></a><a name="iddle0884"></a>Again, the summary mode provides performance statistics about the library calls made during an application's execution. [Table 4-6](ch04lev1sec2.html#ch04table06) describes the meanings of these <a name="iddle0885"></a><a name="iddle0886"></a><a name="iddle0887"></a><a name="iddle0888"></a><a name="iddle0889"></a>statistics.

<a name="ch04table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-6\. CPU-Specific <span class="docEmphasis"><tt>ltrace</tt></span> Output

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>% time</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0890"></a>Of the total time spent making library calls, this is the percentage of time spent on this one.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>seconds</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0891"></a>This is the total number of seconds spent in this library call.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>usecs/call</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0892"></a>This is the number of microseconds spent per library call of this type.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>calls</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0893"></a>This is the total number of calls of this type.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>function</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0894"></a>This is the name of the library call.

</td>

</tr>

</tbody>

</table>

Much like <tt>strace</tt>, <tt>ltrace</tt> has a large number of options that can modify the functions that it traces. These options are described by the <tt>ltrace --help</tt> command and in detail in the <tt>ltrace</tt> man <a name="iddle0895"></a><a name="iddle0896"></a><a name="iddle0897"></a><a name="iddle0898"></a><a name="iddle0899"></a>page.

<a name="ch04lev3sec6"></a>

##### 4.2.3.2 Example Usage

[Listing 4.4](ch04lev1sec2.html#ch04ex04) is a <a name="iddle0900"></a><a name="iddle0901"></a><a name="iddle0902"></a><a name="iddle0903"></a><a name="iddle0904"></a><a name="iddle0905"></a>simple example of <tt>ltrace</tt> running on the <tt>xeyes</tt> command. <tt>xeyes</tt> is an X Window application that pops up a pair of eyes that follow your mouse pointer around the screen.

<a name="ch04ex04"></a>

##### Listing 4.4\.

<pre>[ezolt@localhost manuscript]$	ltrace	-c /usr/X11R6/bin/xeyes

% time	   seconds  usecs/call       calls       function

------ ----------- -----------   ---------  --------------------

 18.65    0.065967       65967           1  XSetWMProtocols

 17.19    0.060803          86         702  hypot

 12.06    0.042654         367         116  XQueryPointer

  9.51    0.033632       33632           1  XtAppInitialize

  8.39    0.029684          84         353  XFillArc

  7.13    0.025204         107         234  cos

  6.24    0.022091          94         234  atan2

  5.56    0.019656          84         234  sin

  4.62    0.016337         139         117  XtAppAddTimeOut

  3.19    0.011297          95         118  XtWidgetToApplicationContext

  3.06    0.010827          91         118  XtWindowOfObject

  1.39    0.004934        4934           1  XtRealizeWidget

  1.39    0.004908        2454           2  XCreateBitmapFromData

  0.65    0.002291        2291           1  XtCreateManagedWidget

  0.12    0.000429         429           1  XShapeQueryExtension

  0.09    0.000332         332           1  XInternAtom

  0.09    0.000327          81           4  XtDisplay

  0.09    0.000320         106           3  XtGetGC

  0.05    0.000168          84           2  XSetForeground

  0.05    0.000166          83           2  XtScreen

  0.04    0.000153         153           1  XtParseTranslationTable

  0.04    0.000138         138           1  XtSetValues

  0.04    0.000129         129           1  XmuCvtStringToBackingStore

  0.03    0.000120         120           1  XtDestroyApplicationContext

  0.03    0.000116         116           1  XtAppAddActions

  0.03    0.000109         109           1  XCreatePixmap

  0.03	  0.000108	   108           1  XtSetLanguageProc

  0.03    0.000104	   104           1  XtOverrideTranslations

  0.03    0.000102         102           1  XtWindow

  0.03	  0.000096          96           1  XtAddConverter

  0.03	  0.000093	    93		 1  XtCreateWindow

  0.03	  0.000093	    93		 1  XFillRectangle

  0.03	  0.000089	    89		 1  XCreateGC

  0.03	  0.000089	    89		 1  XShapeCombineMask

  0.02	  0.000087	    87		 1  XclearWindow

  0.02	  0.000086	    86		 1  XFreePixmap

------ ----------- -----------   ---------  --------------------

100.00	  0.353739	              2261  total

</pre>

In <a name="iddle0906"></a><a name="iddle0907"></a><a name="iddle0908"></a><a name="iddle0909"></a><a name="iddle0910"></a><a name="iddle0911"></a>[Listing 4.4](ch04lev1sec2.html#ch04ex04), the library functions <tt>XSetWMProtocols</tt>, <tt>hypot</tt>, and <tt>XQueryPointer</tt> take 18.65 percent, 17.19 percent, and 12.06 percent of the total time spent in libraries. The call to the second most time-consuming function, <tt>hypot</tt>, is made 702 times, and the call to most time-consuming function, <tt>XSetWMProtocols</tt>, is made only once. Unless our application can completely remove the call to <tt>XSetWMProtocols</tt>, we are likely stuck with whatever time it takes. It is best to turn our attention to <tt>hypot</tt>. Each call to this function is relatively lightweight; so if we can reduce the number of times that it is called, we may be able to speed up the application. <tt>hypot</tt> would probably be the first function to be investigated if the <tt>xeyes</tt> application was a performance problem. Initially, we would determine what <tt>hypot</tt> does, but it is unclear where it may be documented. Possibly, we could figure out which library <tt>hypot</tt> belongs to and read the documentation for that library. In this case, we do not have to find the library first, because a man page exists for the <tt>hypot</tt> function. Running <tt>man hypot</tt> tells us that the hypot function will calculate the distance (hypotenuse) between two points and is part of the math library, <tt>libm</tt>. However, functions in libraries may have no man pages, so we would need to be able to determine what library a function is part of without them. Unfortunately, <tt>ltrace</tt> does not make it at obvious which library a function is from. To figure it out, we have to use the Linux tools <tt>ldd</tt> and <tt>objdump</tt>. First, <tt>ldd</tt> is used to display which libraries are used by a dynamically linked application. Then, <tt>objdump</tt> is used to search each of those libraries for the given function. In [Listing 4.5](ch04lev1sec2.html#ch04ex05), we use <tt>ldd</tt> to see which libraries are used by the <a name="iddle0912"></a><a name="iddle0913"></a><a name="iddle0914"></a><a name="iddle0915"></a><a name="iddle0916"></a><a name="iddle0917"></a><tt>xeyes</tt> application.

<a name="ch04ex05"></a>

##### Listing 4.5\.

<pre>[ezolt@localhost manuscript]$ ldd /usr/X11R6/bin/xeyes

        linux-gate.so.1 => (0x00ed3000)

        libXmu.so.6 => /usr/X11R6/lib/libXmu.so.6 (0x00cd4000)

        libXt.so.6 => /usr/X11R6/lib/libXt.so.6 (0x00a17000)

        libSM.so.6 => /usr/X11R6/lib/libSM.so.6 (0x00368000)

        libICE.so.6 => /usr/X11R6/lib/libICE.so.6 (0x0034f000)

        libXext.so.6 => /usr/X11R6/lib/libXext.so.6 (0x0032c000)

        libX11.so.6 => /usr/X11R6/lib/libX11.so.6 (0x00262000)

        libm.so.6 => /lib/tls/libm.so.6 (0x00237000)

        libc.so.6 => /lib/tls/libc.so.6 (0x0011a000)

        libdl.so.2 => /lib/libdl.so.2 (0x0025c000)

        /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00101000)

</pre>

Now that the <tt>ldd</tt> command has shown the libraries that <tt>xeyes</tt> uses, we can use the <tt>objdump</tt> command to figure out which library the function is in. In [Listing 4.6](ch04lev1sec2.html#ch04ex06), we look for the <tt>hypot</tt> symbol in each of the libraries that <tt>xeyes</tt> is linked to. The <tt>-T</tt> option of <tt>objdump</tt> lists all the symbols (mostly functions) that the library relies on or provides. By using <tt>fgrep</tt> to look at output lines that have <tt>.text</tt> in it, we can see which libraries export the <tt>hypot</tt> function. In this case, we can see that the <tt>libm</tt> library is the only library that contains the <tt>hypot</tt> <a name="iddle0918"></a><a name="iddle0919"></a><a name="iddle0920"></a><a name="iddle0921"></a><a name="iddle0922"></a><a name="iddle0923"></a>function.

<a name="ch04ex06"></a>

##### Listing 4.6\.

<pre>[/tmp]$ objdump -T /usr/X11R6/lib/libXmu.so.6  | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T /usr/X11R6/lib/libXt.so.6   | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T /usr/X11R6/lib/libSM.so.6   | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T /usr/X11R6/lib/libICE.so.6  | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T /usr/X11R6/lib/libXext.so.6 | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T /usr/X11R6/lib/libX11.so.6  | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T  /lib/tls/libm.so.6	       | fgrep ".text"  | grep "hypot"

00247520  w   DF .text  000000a9  GLIBC_2.0    hypotf

0024e810  w   DF .text  00000097  GLIBC_2.0    hypotl

002407c0  w   DF .text  00000097  GLIBC_2.0    hypot

[/tmp]$ objdump -T  /lib/tls/libc.so.6	       | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T  /lib/libdl.so.2	       | fgrep ".text"  | grep "hypot"

[/tmp]$ objdump -T  /lib/ld-linux.so.2	       | fgrep ".text"  | grep "hypot"

</pre>

The next step might be to look through the source of <tt>xeyes</tt> to figure out where <tt>hypot</tt> is called and, if possible, reduce the number of calls made to it. An alternative solution is to look at the source of hypot and try to optimize the source code of the library.

By enabling you to investigate which library calls are taking a long time to complete, <tt>ltrace</tt> enables you to determine the cost of each library call that <a name="iddle0924"></a><a name="iddle0925"></a><a name="iddle0926"></a><a name="iddle0927"></a><a name="iddle0928"></a><a name="iddle0929"></a>an application makes.

<a name="ch04lev2sec7"></a>

#### 4.2.4\. ps (Process Status)

<tt>ps</tt> is an <a name="iddle0930"></a><a name="iddle0931"></a><a name="iddle0932"></a>excellent command to track a process's behavior as it runs.

It provides detailed static and dynamic statistics about currently running processes. <tt>ps</tt> provides static information, such as command name and PID, as well as dynamic information, such as current use of memory and CPU.

<a name="ch04lev3sec7"></a>

##### 4.2.4.1 CPU Performance-Related Options

<tt>ps</tt> has many different options and can retrieve many different statistics about the state of a running application. The following invocations are those options most related to CPU performance and will show information about the given PID:

<pre>ps [-o etime,time,pcpu,command] [-u user] [-U user] [PID]

</pre>

The command ps is probably one of the oldest and feature-rich commands to extract performance information, which can make its use overwhelming. By only looking at a subset of the total functionality, it is much more manageable. [Table 4-7](ch04lev1sec2.html#ch04table07) contains the options that are most relevant to CPU <a name="iddle0933"></a><a name="iddle0934"></a><a name="iddle0935"></a>performance.

<a name="ch04table07"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-7\. <span class="docEmphasis">ps</span> Command-Line Options

</caption><colgroup><col width="100"><col width="100"><col width="100"><col width="200"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-o <statistic></tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="3">

<a name="iddle0936"></a>This option enables you to specify exactly what process statistics you want to track. The different statistics are specified in a comma-separated list with no spaces.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>etime</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="2">

<a name="iddle0937"></a>Statistic: Elapsed time is the amount of time since the program began execution.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>time</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="2">

<a name="iddle0938"></a>Statistic: CPU time is the amount of system plus user time the process spent running on the CPU.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pcpu</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="2">

<a name="iddle0939"></a>Statistic: The percentage of CPU that the process is currently consuming.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>command</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="2">

<a name="iddle0940"></a>Statistic: This is the command name.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-A</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0941"></a>Shows statistics about all processes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-u user</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0942"></a>Shows statistics about all processes with this effective user ID.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-U user</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0943"></a>Shows statistic about all processes with this user ID.

</td>

</tr>

</tbody>

</table>

<a name="iddle0944"></a><a name="iddle0945"></a><a name="iddle0946"></a><tt>ps</tt> provides myriad different performance statistics in addition to CPU statistics, many of which, such as a process's memory usage, are discussed in subsequent chapters.

<a name="ch04lev3sec8"></a>

##### 4.2.4.2 Example Usage

This <a name="iddle0947"></a><a name="iddle0948"></a><a name="iddle0949"></a>example shows a test application that is consuming 88 percent of the CPU and has been running for 6 seconds, but has only consumed 5 seconds of CPU time:

<pre>[ezolt@wintermute tmp]$ ps -o etime,time,pcpu,cmd 10882

    ELAPSED     TIME %CPU CMD

      00:06 00:00:05 88.0 ./burn

</pre>

In [Listing 4.7](ch04lev1sec2.html#ch04ex07), instead of investigating the CPU performance of a particular process, we look at all the processes that a particular user is running. This may reveal information about the amount of resources a particular user consumes. In this case, we look at all the processes that the <tt>netdump</tt> user is running. Fortunately, <tt>netdump</tt> is a tame user and is only running bash, which is not taking up any of the CPU, and top, which is only taking up 0.5 percent of the <a name="iddle0950"></a><a name="iddle0951"></a><a name="iddle0952"></a>CPU.

<a name="ch04ex07"></a>

##### Listing 4.7\.

<pre>[/tmp]$ ps -o time,pcpu,command -u netdump

    TIME %CPU COMMAND

00:00:00  0.0 -bash

00:00:00  0.5 top

</pre>

Unlike <tt>time</tt>, ps enables us to monitor information about a process currently running. For long-running jobs, you can use <tt>ps</tt> to periodically check the status of the process (instead of using it only to provide statistics about the program's execution after it has <a name="iddle0953"></a><a name="iddle0954"></a><a name="iddle0955"></a>completed).

<a name="ch04lev2sec8"></a>

#### 4.2.5\. ld.so (Dynamic Loader)

When a dynamically <a name="iddle0956"></a><a name="iddle0957"></a><a name="iddle0958"></a>linked application is executed, the Linux loader, <tt>ld.so</tt>, runs first. <tt>ld.so</tt> loads all the application's libraries and connects symbols that the application uses with the functions the libraries provide. Because different libraries were originally linked at different and possibly overlapping places in memory, the linker needs to sort through all the symbols and make sure that each lives at a different place in memory. When a symbol is moved from one virtual address to another, this is called a relocation. It takes time for the loader to do this, and it is much better if it does not need to be done at all. The prelink application aims to do that by rearranging the system libraries of the entire systems so that they do not overlap. An application with a high number of relocations may not have been prelinked.

The Linux loader usually runs without any intervention from the user, and by just executing a dynamic program, it is run automatically. Although the execution of the loader is hidden from the user, it still takes time to run and can potentially slow down an application's startup time. When you ask for loader statistics, the loader shows the amount of work it is doing and enables you to figure out whether it is a <a name="iddle0959"></a><a name="iddle0960"></a><a name="iddle0961"></a>bottleneck.

<a name="ch04lev3sec9"></a>

##### 4.2.5.1 CPU Performance-Related Options

The <tt>ld</tt> command <a name="iddle0962"></a><a name="iddle0963"></a><a name="iddle0964"></a>is invisibly run for every Linux application that uses shared libraries. By setting the appropriate environment variables, we can ask it to dump information about its execution. The following invocation influences <tt>ld</tt> execution:

<pre>env LD_DEBUG=statistics,help LD_DEBUG_OUTPUT=filename <command>

</pre>

The debugging capabilities of the loader are completely controlled <a name="iddle0965"></a><a name="iddle0966"></a><a name="iddle0967"></a><a name="iddle0968"></a>with environmental variables. [Table 4-8](ch04lev1sec2.html#ch04table08) describes these variables.

<a name="ch04table08"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-8\. <span class="docEmphasis"><tt>ld</tt></span> Environmental Variables

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>LD_DEBUG=statistics</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This turns on the display of statistics for <tt>ld</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>LD_DEBUG=help</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays information about the available debugging statistics.

</td>

</tr>

</tbody>

</table>

<a name="iddle0969"></a><a name="iddle0970"></a><a name="iddle0971"></a><a name="iddle0972"></a>[Table 4-9](ch04lev1sec2.html#ch04table09) describes some of the statistics that <tt>ld.so</tt> can provide. Time is given in clock cycles. To convert this to wall time, you must divide by the processor's clock speed. (This information is available from <tt>cat /proc/cpuinfo</tt>.)

<a name="ch04table09"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-9\. CPU Specific <span class="docEmphasis"><tt>ld.so</tt></span> Output

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0973"></a><a name="iddle0974"></a><a name="iddle0975"></a>Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>total startup time in dynamic loader</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total amount of time (in clock cycles) spent in the load before the application started to execute.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>time needed for relocation</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total amount of time (in clock cycles) spent relocating symbols.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>number of relocations</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of new relocation calculations done before the application's execution began.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>number of relocations from cache</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of relocations that were precalculated and used before the application started to execute.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>number of relative <tt>relocations</tt></tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of relative relocations.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>time needed to load objects</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The time needed to load all the libraries that an application is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>final number of relocations</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total number of relocations made during an application run (including those made by <tt>dlopen</tt>).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>final number of relocations from cache</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total number of relocations that were precalculated.

</td>

</tr>

</tbody>

</table>

The information provided by <tt>ld</tt> can prove helpful in determining how much time is being spent setting up dynamic libraries before an application <a name="iddle0976"></a><a name="iddle0977"></a><a name="iddle0978"></a>begins executing.

<a name="ch04lev3sec10"></a>

##### 4.2.5.2 Example Usage

In [Listing 4.8](ch04lev1sec2.html#ch04ex08), we run an application with the <tt>ld</tt> debugging environmental variables defined. The output statistics are saved into the <tt>lddebug</tt> file. Notice that the loader shows two different sets of statistics. The first shows all the relocations that happen during startup, whereas the last shows all the statistics after the program closes. These can be different values if the application uses functions such as <tt>dlopen</tt>, which allows shared libraries to be mapped into an application after it has started to execute. In this case, we see that 83 percent of the time spent in the loader was doing allocations. If the application had been prelinked, this would have dropped close to zero.

<a name="ch04ex08"></a>

##### Listing 4.8\.

<pre>[ezolt@wintermute ezolt]$ env LD_DEBUG=statistics LD_DEBUG_OUTPUT=lddebug gcalctool

[ezolt@wintermute ezolt]$ cat lddebug.2647

     2647:

     2647:     runtime linker statistics:

     2647:       total startup time in dynamic loader: 40820767 clock cycles

     2647:                 time needed for relocation: 33896920 clock cycles (83.0%)

     2647:                      number of relocations: 2821

     2647:           number of relocations from cache: 2284

     2647:             number of relative relocations: 27717

     2647:                time needed to load objects: 6421031 clock cycles (15.7%)

     2647:

     2647:     runtime linker statistics:

     2647:                final number of relocations: 6693

     2647:     final number of relocations from cache: 2284

</pre>

If <tt>ld</tt> is determined to be the cause of sluggish startup time, it may be possible to reduce the amount of startup time by pruning the number of libraries that an application relies on or running <tt>prelink</tt> on the <a name="iddle0979"></a><a name="iddle0980"></a><a name="iddle0981"></a>system.

<a name="ch04lev2sec9"></a>

#### 4.2.6\. gprof

A powerful way to profile <a name="iddle0982"></a><a name="iddle0983"></a><a name="iddle0984"></a><a name="iddle0985"></a>applications on Linux is to use the <tt>gprof</tt> profiling command. <tt>gprof</tt> can show the call graph of application and sample where the application time is spent. <tt>gprof</tt> works by first instrumenting your application and then running the application to generate a sample file. <tt>gprof</tt> is very powerful, but requires application source and adds instrumentation overhead. Although it can accurately determine the number of times a function is called and approximate the amount of time spent in a function, the <tt>gprof</tt> instrumentation will likely change the timing characteristics of the application and slow down its execution.

<a name="ch04lev3sec11"></a>

##### 4.2.6.1 CPU Performance-Related Options

To profile an application with <tt>gprof</tt>, you <a name="iddle0986"></a><a name="iddle0987"></a><a name="iddle0988"></a><a name="iddle0989"></a>must have access to application source. You must then compile that application with a <tt>gcc</tt> command similar to the following:

<pre>gcc -gp -g3 -o app app.c

</pre>

First, you must compile the application with profiling turned on, using <tt>gcc's -gp</tt> option. You must take care not to strip the executable, and it is even more helpful to turn on symbols when compiling using the <tt>-g3</tt> option. Symbol information is necessary to use the source annotation feature of <tt>gprof</tt>. When you run your instrumented application, an output file is generated. You can then use the gprof command to display the results. The <tt>gprof</tt> command is invoked as follows:

<pre>gprof [-p –flat-profile -q --graph --brief -A –annotated-source ] app

</pre>

The options described in [Table 4-10](ch04lev1sec2.html#ch04table10) specify what information gprof <a name="iddle0990"></a><a name="iddle0991"></a><a name="iddle0992"></a><a name="iddle0993"></a>displays.

<a name="ch04table10"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-10\. <span class="docEmphasis"><tt>gprof</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--brief</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0994"></a>This option abbreviates the output of <tt>gprof</tt>. By default, <tt>gprof</tt> prints out all the performance information and a legend to describe what each metric means. This suppresses the legend.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p <a name="iddle0995"></a>or --flat-profile</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0996"></a>This option prints out the total amount of time spent and the number of calls to each function in the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-q <a name="iddle0997"></a>or --graph</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0998"></a>This option prints out a call graph of the profiled application. This shows how the functions in the program called each other, how much time was spent in each of the functions, and how much was spent in the functions of the children.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-A <a name="iddle0999"></a>or --annotated-source</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1000"></a>This shows the profiling information next to the original source code.

</td>

</tr>

</tbody>

</table>

Not all the output statistics are available for a particular profile. Which output statistic is available depends on how the application was compiled <a name="iddle1001"></a><a name="iddle1002"></a><a name="iddle1003"></a><a name="iddle1004"></a>for profiling.

<a name="ch04lev3sec12"></a>

##### 4.2.6.2 Example Usage

When profiling <a name="iddle1005"></a><a name="iddle1006"></a><a name="iddle1007"></a><a name="iddle1008"></a>an application with <tt>gprof</tt>, the first step is to compile the application with profiling information. The compiler (<tt>gcc</tt>) inserts profiling information into the application and, when the application is run, it is saved into a file named <tt>gmon.out</tt>. The burn test application is fairly simple. It clears a large area of memory and then calls two functions, <tt>a()</tt> and <tt>b()</tt>, which each touch this memory. Function <tt>a()</tt> touches the memory 10 times as often as function <tt>b()</tt>.

First, we compile the application:

<pre>[ezolt@wintermute test_app]$ gcc -pg -g3 -o burn_gprof burn.c

</pre>

After we run in it, we can analyze the output. This is shown in <a name="iddle1009"></a><a name="iddle1010"></a><a name="iddle1011"></a><a name="iddle1012"></a>[Listing 4.9](ch04lev1sec2.html#ch04ex09).

<a name="ch04ex09"></a>

##### Listing 4.9\.

<pre>[ezolt@wintermute test_app]$ gprof  --brief -p ./burn_gprof

Flat profile:

Each sample counts as 0.01 seconds.

  %   cumulative   self              self     total

 time   seconds   seconds    calls   s/call   s/call  name

 91.01      5.06     5.06        1     5.06     5.06  a

  8.99      5.56     0.50        1     0.50     0.50  b

</pre>

In [Listing 4.9](ch04lev1sec2.html#ch04ex09), you can see <tt>gprof</tt> telling us what we already knew about the application. It has two functions, <tt>a()</tt> and <tt>b()</tt>. Each function is called once, and <tt>a()</tt> takes 10 times (91 percent) the amount of time to complete than <tt>b()</tt> (8.99 percent). 5.06 seconds of time is spent in the function <tt>a()</tt>, and .5 seconds is spent in function <tt>b()</tt>.

[Listing 4.10](ch04lev1sec2.html#ch04ex10) shows the call graph for the test application. The <tt><spontaneous></tt> comment listed in the output means that although <tt>gprof</tt> did not record any samples in <tt>main()</tt>, it deduced that <tt>main()</tt> must have been run, because functions <tt>a()</tt> and <tt>b()</tt> both had samples, and <tt>main</tt> was the only function in the code that called them. <tt>gprof</tt> most likely did not record any samples in <tt>main()</tt> because it is a very <a name="iddle1013"></a><a name="iddle1014"></a><a name="iddle1015"></a><a name="iddle1016"></a>short function.

<a name="ch04ex10"></a>

##### Listing 4.10\.

<pre>[ezolt@wintermute test_app]$ gprof  --brief -q ./burn_gprof

                  Call graph

granularity: each sample hit covers 4 byte(s) for 0.18% of 5.56 seconds

index % time    self  children    called     name

                                                 <spontaneous>

[1]    100.0    0.00    5.56                 main [1]

                5.06    0.00       1/1           a [2]

                0.50    0.00       1/1           b [3]

-----------------------------------------------

                5.06    0.00       1/1           main [1]

[2]     91.0    5.06    0.00       1         a [2]

-----------------------------------------------

                0.50    0.00       1/1           main [1]

[3]     9.0     0.50    0.00       1         b [3]

-----------------------------------------------

Index by function name

   [2] a                       [3] b

</pre>

Finally, <tt>gprof</tt> can annotate the source code to show how often each function is called. Notice that [Listing 4.11](ch04lev1sec2.html#ch04ex11) does not show the time spent in the function; instead, it shows the number of times the function was called. As shown in the previous examples for <tt>gprof</tt>, <tt>a()</tt> actually took 10 times as long as <tt>b()</tt>, so be careful when optimizing. Do not assume that functions that are called a large number of times are actually using the CPU for a large amount of time or that functions that are called a few number of times are necessarily taking a small amount of the <a name="iddle1017"></a><a name="iddle1018"></a><a name="iddle1019"></a><a name="iddle1020"></a>CPU time.

<a name="ch04ex11"></a>

##### Listing 4.11\.

<pre>[ezolt@wintermute test_app]$ gprof -A burn_gprof

*** File /usr/src/perf/process_specific/test_app/burn.c:

                #include <string.h>

                #define ITER 10000

                #define SIZE 10000000

                #define STRIDE 10000

                char test[SIZE];

                void a(void)

           1 -> {

                  int i=0,j=0;

                  for (j=0;j<10*ITER ; j++)

                    for (i=0;i<SIZE;i=i+STRIDE)

                      {

                        test[i]++;

                      }

                }

                void b(void)

           1 -> {

                  int i=0,j=0;

                  for (j=0;j<ITER; j++)

                    for (i=0;i<SIZE;i=i+STRIDE)

                      {

                        test[i]++;

                      }

                }

                main()

       ##### -> {

                  /* Arbitrary value*/

                  memset(test, 42, SIZE);

                  a();

                  b();

               }

Top 10 Lines:

     Line      Count

       10          1

       20          1

Execution Summary:

        3   Executable lines in this file

        3   Lines executed

   100.00   Percent of the file executed

       2    Total number of line executions

    0.67    Average executions per line

</pre>

<tt>gprof</tt> provides a good summary of how many times functions or source lines in an application have been run and how long <a name="iddle1021"></a><a name="iddle1022"></a><a name="iddle1023"></a><a name="iddle1024"></a>they took.

<a name="ch04lev2sec10"></a>

#### 4.2.7\. oprofile (II)

As discussed in [Chapter 2](ch02.html#ch02), "[Performance Tools: System CPU](ch02.html#ch02)," you can use <tt>oprofile</tt> to track down the location of different events in the system or an application. <tt>oprofile</tt> is a lower-overhead tool than <tt>gprof</tt>. Unlike <tt>gprof</tt>, it does not require an application to be recompiled to be used. <tt>oprofile</tt> can also measure events not supported by <tt>gprof</tt>. Currently, <tt>oprofile</tt> can only support call graphs like those that <tt>gprof</tt> can generate with a kernel patch, whereas <tt>gprof</tt> can run on any Linux kernel.

<a name="ch04lev3sec13"></a>

##### 4.2.7.1 CPU Performance-Related Options

The <tt>oprofile</tt> discussion <a name="iddle1025"></a><a name="iddle1026"></a><a name="iddle1027"></a><a name="iddle1028"></a>in the section, "System-Wide Performance Tools" in [Chapter 2](ch02.html#ch02) covers how to start profiling with <tt>oprofile</tt>. This section describes the parts of <tt>oprofile</tt> used to analyze the results of process-level sampling.

<tt>oprofile</tt> has a series of tools that display samples that have been collected. The first <a name="iddle1029"></a>tool, <tt>opreport</tt>, displays information about how samples are distributed to the functions within executables and libraries. It is invoked as follows:

<pre>opreport [-d --details -f --long-filenames -l --symbols -l] application

</pre>

[Table 4-11](ch04lev1sec2.html#ch04table11) describes a few commands that can modify the level <a name="iddle1030"></a><a name="iddle1031"></a><a name="iddle1032"></a><a name="iddle1033"></a><a name="iddle1034"></a>of information that opreport provides.

<a name="ch04table11"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-11\. <span class="docEmphasis"><tt>opreport</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1035"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d <a name="iddle1036"></a>or --details</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1037"></a>This shows an instruction-level breakdown of all the collected samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-f <a name="iddle1038"></a>or --long-filenames</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1039"></a>This shows the complete path name of the application being analyzed.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-l <a name="iddle1040"></a>or --symbols</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1041"></a>This shows how an application's samples are distributed to its symbols. This enables you to see what functions have the most samples attributed to them.

</td>

</tr>

</tbody>

</table>

<a name="iddle1042"></a><a name="iddle1043"></a><a name="iddle1044"></a><a name="iddle1045"></a>The next command that you can use to extract information about performance samples <a name="iddle1046"></a><a name="iddle1047"></a><a name="iddle1048"></a><a name="iddle1049"></a><a name="iddle1050"></a>is <tt>opannotate</tt>. <tt>opannotate</tt> can attribute samples to specific source lines or assembly instructions. It is invoked as follows:

<pre>opannotate [-a --assembly] [-s --source] application

</pre>

The options described in [Table 4-12](ch04lev1sec2.html#ch04table12) enable you to specify exactly what information <tt>opannotate</tt> will provide. One word of caution: because of limitations in the processor hardware counters at the source line and instruction level, the sample attributions may not be on the exact line that caused them; however, they will be near the actual event.

<a name="ch04table12"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 4-12\. <span class="docEmphasis"><tt>opannotate</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-s <a name="iddle1051"></a>or --source --</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1052"></a>This shows the collected samples next to the application's source code.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-a <a name="iddle1053"></a>or --assembly</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1054"></a>This shows the samples collected next to the assembly code of the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1055"></a><tt>-s and -a</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1056"></a>If both <tt>-s</tt> and <tt>-a</tt> are specified, <tt>opannotate</tt> intermingles the source and assembly code with the samples.

</td>

</tr>

</tbody>

</table>

When <a name="iddle1057"></a><a name="iddle1058"></a><a name="iddle1059"></a><a name="iddle1060"></a><a name="iddle1061"></a><a name="iddle1062"></a><a name="iddle1063"></a>using <tt>opannotate</tt> and <tt>opreport</tt>, it is always best to specify the full path name to the application. If you do not, you may receive a cryptic error message (if <tt>oprofile</tt> cannot find the application's samples). By default, when displaying results, <tt>opreport</tt> only shows the executable name, which can be ambiguous in a system with multiple executables or libraries with identical names. Always specify the <tt>-f</tt> option so that <tt>opreport</tt> shows the complete path to the application.

<tt>oprofile</tt> also provides a command, <tt>opgprof</tt>, that can export the samples collected by <tt>oprofile</tt> into a form that <tt>gprof</tt> can digest. It is invoked in the following way:

<pre>opgprof application

</pre>

This command takes the samples of <tt>application</tt> and generates a <tt>gprof</tt>-compatible profile. You can then view this file with the <a name="iddle1064"></a><a name="iddle1065"></a><a name="iddle1066"></a><a name="iddle1067"></a><a name="iddle1068"></a><a name="iddle1069"></a><a name="iddle1070"></a><tt>gprof</tt> command.

<a name="ch04lev3sec14"></a>

##### 4.2.7.2 Example Usage

Because we <a name="iddle1071"></a><a name="iddle1072"></a><a name="iddle1073"></a><a name="iddle1074"></a>already looked at <tt>oprofile</tt> in the section, "System-Wide Performance Tools" in [Chapter 2](ch02.html#ch02), the examples here show you how to use <tt>oprofile</tt> to track down a performance problem to a particular line of source code. This section assumes that you have already started the profiling using the <tt>opcontrol</tt> command. The next step is to run the program that is having the performance problem. In this case, we use the burn program, which is the same that we used in the <tt>gprof</tt> example. We start our test program as follows:

<pre>[ezolt@wintermute tmp]$ ./burn

</pre>

After the program finishes, we must dump <tt>oprofile's</tt> buffers to disk, or else the samples will not be available to <tt>opreport</tt>. We do that using the following command:

<pre>[ezolt@wintermute tmp]$ sudo opcontrol -d

</pre>

Next, in [Listing 4.12](ch04lev1sec2.html#ch04ex12) we ask <a name="iddle1075"></a><tt>opreport</tt> to tell us about the samples relevant to our test application, <tt>/tmp/burn</tt>. This gives us an overall view of how many cycles our application consumed. In this case, we see that 9,939 samples were taken for our application. As we dig into the <tt>oprofile</tt> tools, we will see how these samples are distributed within the burn <a name="iddle1076"></a><a name="iddle1077"></a><a name="iddle1078"></a><a name="iddle1079"></a>application.

<a name="ch04ex12"></a>

##### Listing 4.12\.

<pre>[ezolt@wintermute tmp]$ opreport -f /tmp/burn

CPU: PIII, speed 467.731 MHz (estimated)

Counted CPU_CLK_UNHALTED events (clocks processor is not halted) with a

unit mask of 0x00 (No unit mask) count 233865

     9939 100.0000 /tmp/burn

</pre>

Next, in [Listing 4.13](ch04lev1sec2.html#ch04ex13), we want to see which functions in the burn application had all the samples. Because we are using the <tt>CPU_CLK_UNHALTED</tt> event, this roughly corresponds to the relative amount of time spent in each function. By looking at the output, we can see that 91 percent of the time was spent in function <tt>a()</tt>, and 9 percent was spent in function <tt>b()</tt>.

<a name="ch04ex13"></a>

##### Listing 4.13\.

<pre>[ezolt@wintermute tmp]$ opreport -l /tmp/burn

CPU: PIII, speed 467.731 MHz (estimated)

Counted CPU_CLK_UNHALTED events (clocks processor is not halted) with a

unit mask of 0x00 (No unit mask) count 233865

vma      samples %           symbol name

08048348 9033    90.9118     a

0804839e 903      9.0882     b

</pre>

In [Listing 4.14](ch04lev1sec2.html#ch04ex14), we ask <tt>opreport</tt> <a name="iddle1080"></a>to show us which virtual addresses have samples attributed to them. In this case, it appears as if the instruction at address 0x0804838a has 75 percent of the samples. However, it is currently unclear what this instruction is doing or <a name="iddle1081"></a><a name="iddle1082"></a><a name="iddle1083"></a><a name="iddle1084"></a>why.

<a name="ch04ex14"></a>

##### Listing 4.14\.

<pre>[ezolt@wintermute tmp]$ opreport -d /tmp/burn

CPU: PIII, speed 467.731 MHz (estimated)

Counted CPU_CLK_UNHALTED events (clocks processor is not halted) with a

unit mask of 0x00 (No unit mask) count 233865

vma      samples  %           symbol name

08048348 9033     90.9118     a

 08048363 4        0.0443

 08048375 431      4.7714

 0804837c 271      3.0001

 0804837e 1        0.0111

 08048380 422      4.6718

 0804838a 6786    75.1245

 08048393 1114    12.3326

 08048395 4        0.0443

0804839e 903      9.0882      b

 080483cb 38       4.2082

 080483d2 19       2.1041

 080483d6 50       5.5371

 080483e0 697     77.1872

 080483e9 99      10.9635

</pre>

Generally, it is more useful to know the source line that is using all the CPU time rather than the virtual address of the instruction that is using it. It is not always easy to figure out the correspondence between a source line and a particular instruction; so, in [Listing 4.15](ch04lev1sec2.html#ch04ex15), we ask <tt>opannotate</tt> <a name="iddle1085"></a>to do the hard work and show us the samples relative to the original source code (rather than the instruction's <a name="iddle1086"></a><a name="iddle1087"></a><a name="iddle1088"></a><a name="iddle1089"></a>virtual address).

<a name="ch04ex15"></a>

##### Listing 4.15\.

<pre>[ezolt@wintermute tmp]$ opannotate --source /tmp/burn

/*

 * Command line: opannotate --source /tmp/burn

 *

 * Interpretation of command line:

 * Output annotated source file with samples

 * Output all files

 *

 * CPU: PIII, speed 467.731 MHz (estimated)

 * Counted CPU_CLK_UNHALTED events (clocks processor is not halted) with

a unit mask of 0x00 (No unit mask) count 233865

 */

/*

 * Total samples for file : "/tmp/burn.c"

 *

 *   9936 100.0000

 */

               :#include <string.h>

               :

               :#define ITER 10000

               :#define SIZE 10000000

               :#define STRIDE 10000

               :

               :char test[SIZE];

               :

               :void a(void)

               :{ /* a total:   9033 90.9118 */

               :  int i=0,j=0;

     8  0.0805 :  for (j=0;j<10*ITER ; j++)

  8603 86.5841 :    for (i=0;i<SIZE;i=i+STRIDE)

               :      {

   422  4.2472 :        test[i]++;

               :      }

               :}

               :

               :void b(void)

               :{ /* b total:       903  9.0882 */

               :  int i=0,j=0;

               :  for (j=0;j<ITER; j++)

   853  8.5849 :    for (i=0;i<SIZE;i=i+STRIDE)

               :      {

    50  0.5032 :        test[i]++;

               :      }

               :}

               :

               :

               :main()

               :{

               :

               :  /* Arbitrary value*/

               :  memset(test, 42, SIZE);

               :  a();

               :  b();

               :}

</pre>

As you <a name="iddle1090"></a><a name="iddle1091"></a><a name="iddle1092"></a><a name="iddle1093"></a>can see in [Listing 4.15](ch04lev1sec2.html#ch04ex15), <tt>opannotate</tt> attributes most of the samples (86.59 percent) to the <tt>for</tt> loop in function <tt>b()</tt>. Unfortunately, this is a portion of the <tt>for</tt> loop that should not be expensive. Adding a fixed amount to an integer is very fast on modern processors, so the samples that <tt>oprofile</tt> reported were likely attributed to the wrong source line. The line below, <tt>test[i]++;</tt>, should be very expensive because it accesses the memory subsystem. This line is where the samples should have been attributed.

<tt>oprofile</tt> can mis-attribute samples for a few reasons beyond its control. First, the processor does not always interrupt on the exact line that caused the event to occur. This may cause samples to be attributed to instructions near the cause of the event, rather than to the exact instruction that caused the event. Second, when source code is compiled, compilers often rearrange instructions to make the executable more efficient. After a compiler has finished optimizing, code may not execute in the order that it was written. Separate source lines may have been rearranged and combined. As a result, a particular instruction may be the result of more than one source line, or may even be a compiler-generated intermediate piece of code that does not exist in the original source. As a result, when the compiler optimizes the code and generates machine instructions, there may no longer be a one-to-one mapping between the original lines of source code and the generated machine instructions. This can make it difficult or impossible for <tt>oprofile</tt> (and debuggers) to figure out exactly which line of source code corresponds to each machine instruction. However, <tt>oprofile</tt> tries to be as close as possible, so you can usually look a few lines above and below the line with the high sample count and figure out which code is truly expensive. If necessary, you can use <tt>opannotate</tt> to show the exact assembly instructions and virtual addresses that are receiving all the samples. It may be possible to figure out what the assembly instructions are doing and then map it back to your original source code by hand. <tt>oprofile</tt>'s sample attribution is not perfect, but it is usually close enough. Even with these limitations, the profiles provided by <tt>oprofile</tt> show the approximate source line to investigate, which is usually enough to figure out where the application is slowing <a name="iddle1094"></a><a name="iddle1095"></a><a name="iddle1096"></a><a name="iddle1097"></a>down.

<a name="ch04lev2sec11"></a>

#### 4.2.8\. Languages: Static (C and C++) Versus Dynamic (Java and Mono)

The majority of the Linux performance tools support analysis of static languages <a name="iddle1098"></a><a name="iddle1099"></a><a name="iddle1100"></a><a name="iddle1101"></a><a name="iddle1102"></a>such as C and C++, and all the tools described in this chapter work with applications written in these languages. The tools <tt>ltrace</tt>, <tt>strace</tt>, and <tt>time</tt> work with applications written in dynamic languages such as Java, Mono, Python, or Perl. However, the profiling tools <tt>gprof</tt> and <tt>oprofile</tt> cannot be used with these types of applications. Fortunately, most dynamic languages provide non-Linux–specific profiling infrastructures that you can use to generate similar types of profiles.

For Java applications, if the <tt>java</tt> command is run with the <tt>-Xrunhprof</tt> command-line option, <a name="iddle1103"></a><a name="iddle1104"></a><tt>-Xrunhprof</tt> profiles the application. More details are available at [http://antprof.sourceforge.net/hprof.html](http://antprof.sourceforge.net/hprof.html). For Mono applications, if the <tt>mono</tt> executable is passed the <tt>--profile</tt> flag, it profiles the application. More details are available at [http://www.go-mono.com/performance.html](http://www.go-mono.com/performance.html). Perl <a name="iddle1105"></a>and Python <a name="iddle1106"></a>have similar profile functionality, with Perl's <tt>Devel::DProf</tt> described at [http://www.perl.com/pub/a/2004/06/25/profiling.html](http://www.perl.com/pub/a/2004/06/25/profiling.html), and Python's <tt>profiler</tt> described at [http://docs.python.org/lib/profile.html](http://docs.python.org/lib/profile.html), <a name="iddle1107"></a><a name="iddle1108"></a><a name="iddle1109"></a><a name="iddle1110"></a><a name="iddle1111"></a>respectively.