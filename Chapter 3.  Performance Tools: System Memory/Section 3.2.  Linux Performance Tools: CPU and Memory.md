### 3.2\. Linux Performance Tools: CPU and Memory

Here begins our discussion of performance tools that enable you to extract the memory performance information described previously.

<a name="ch03lev2sec3"></a>

#### 3.2.1\. vmstat (Virtual Memory Statistics) II

As you have <a name="iddle0451"></a><a name="iddle0452"></a><a name="iddle0453"></a>seen before, <tt>vmstat</tt> can provide information about many different performance aspects of a system—although its primary purpose, as shown next, is to provide information about virtual memory system performance. In addition to the CPU performance statistics described in the previous chapter, it can also tell you the following:

*   How much swap is being used

*   How the physical memory is being used

*   How much memory is free

As you can see, vmstat provides (via the statistics it displays) a wealth of information about the health and performance of the system in a single line of text.

<a name="ch03lev3sec6"></a>

##### 3.2.1.1 System-Wide Memory-Related Options

In addition to the CPU statistics <a name="iddle0454"></a><a name="iddle0455"></a><a name="iddle0456"></a><tt>vmstat</tt> can provide, you can invoke <tt>vmstat</tt> with the following command-line options when investigating memory statistics:

<pre>vmstat [-a] [-s] [-m]

</pre>

As before, you can run <tt>vmstat</tt> in two modes: sample mode <a name="iddle0457"></a><a name="iddle0458"></a><a name="iddle0459"></a><a name="iddle0460"></a><a name="iddle0461"></a><a name="iddle0462"></a><a name="iddle0463"></a>and average mode. The added command-line options enable you to get the performance statistics about how the Linux kernel is using memory. [Table 3-1](ch03lev1sec2.html#ch03table01) describes the options that <tt>vmstat</tt> accepts.

<a name="ch03table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-1\. <span class="docEmphasis"><tt>vmstat</tt></span> Command-Line Options

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0464"></a><a name="iddle0465"></a><a name="iddle0466"></a><a name="iddle0467"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-a</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0468"></a>This changes the default output of memory statistics to indicate the active/inactive amount of memory rather than information about buffer and cache usage.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0469"></a><tt>-s</tt> (<tt>procps</tt> 3.2 or greater)

</td>

<td class="docTableCell" align="left" valign="top">

This prints out the <tt>vm</tt> table. This is a grab bag of differentstatistics about the system since it has booted. It cannot be run in sample mode. It contains both memory and CPU statistics.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0470"></a><tt>-m</tt> (<tt>procps</tt> 3.2 or greater)

</td>

<td class="docTableCell" align="left" valign="top">

This prints out the kernel's slab info. This is the same information that can be retrieved by typing <tt>cat/proc/slabinfo</tt>. This describes in detail how the kernel's memory is allocated and can be helpful to determine what area of the kernel is consuming the most memory.

</td>

</tr>

</tbody>

</table>

[Table 3-2](ch03lev1sec2.html#ch03table02) provides a list of the <a name="iddle0471"></a><a name="iddle0472"></a><a name="iddle0473"></a>memory statistics that <tt>vmstat</tt> can provide. As with the CPU statistics, when run in normal mode, the first line that <tt>vmstat</tt> provides is the average values for all the rate statistics (<tt>so</tt> and <tt>si</tt>) and the instantaneous value for all the numeric statistics (<tt>swpd</tt>, <tt>free</tt>, <tt>buff</tt>, <tt>cache</tt>, <tt>active</tt>, and <tt>inactive</tt>).

<a name="ch03table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-2\. Memory-Specific <span class="docEmphasis"><tt>vmstat</tt></span> Output Statistics

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

<tt>swpd</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0474"></a>The total amount of memory currently swapped to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0475"></a>The amount of physical memory not being used by the operating system or applications.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>buff</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0476"></a>The size (in KB) of the system buffers, or memory used to store data waiting to be saved to disk. This memory allows an application to continue execution immediately after it has issued a write call to the Linux kernel (instead of waiting until the data has been committed to disk).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>cache</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0477"></a>The size (in KB) of the system cache or memory used to store data previously read from disk. If an application needs this data again, it allows the kernel to fetch it from memory rather than disk, thus increasing performance.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>active</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0478"></a>The amount of memory actively being used. The active/ inactive statistics are orthogonal to the buffer/cache; buffer and cache memory can be active and inactive.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>inactive</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0479"></a>The amount of inactive memory (in KB), or memory that has not been used for a while and is eligible to be swapped to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>si</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0480"></a>The rate of memory (in KB/s) that has been swapped in from disk during the last sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>so</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0481"></a>The rate of memory (in KB/s) that has been swapped out to disk during the last sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pages paged in</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0482"></a>The amount of memory (in pages) read from the disk(s) into the system buffers. (On most IA32 systems, a page is 4KB.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pages paged out</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0483"></a>The amount of memory (in pages) written to the disk(s) from the system cache. (On most IA32 systems, a page is 4KB.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pages swapped in</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0484"></a>The amount of memory (in pages) read from swap into system memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pages swapped in/out</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0485"></a>The amount of memory (in pages) written from system memory to the swap.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>used swap</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0486"></a>The amount of swap currently being used by the Linux kernel.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>free swap</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0487"></a>The amount of swap currently available for use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>total swap</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0488"></a>The total amount of swap that the system has; this is also the sum of used swap plus free swap.

</td>

</tr>

</tbody>

</table>

<tt>vmstat</tt> provides a <a name="iddle0489"></a><a name="iddle0490"></a><a name="iddle0491"></a>good overview of the current state of the virtual memory system for a given machine. Although it does not provide a complete and detailed list of every Linux memory performance statistic available, it does provide a compact output that can indicate how the system memory is being used overall.

<a name="ch03lev3sec7"></a>

##### 3.2.1.2 Example Usage

In [Listing 3.2](ch03lev1sec2.html#ch03ex02), as <a name="iddle0492"></a><a name="iddle0493"></a><a name="iddle0494"></a>you saw in the previous chapter, if <tt>vmstat</tt> is invoked without any command-line options, it displays average values for performance statistics since system boot (<tt>si</tt> and <tt>so</tt>), and it shows the instantaneous values for the rest of them (<tt>swpd</tt>, <tt>free</tt>, <tt>buff</tt>, and <tt>cache</tt>). In this <a name="iddle0495"></a><a name="iddle0496"></a><a name="iddle0497"></a><a name="iddle0498"></a><a name="iddle0499"></a><a name="iddle0500"></a><a name="iddle0501"></a><a name="iddle0502"></a><a name="iddle0503"></a>case, we can see that the system has about 500MB of memory that has been swapped to disk. ~14MB of the system memory is free. ~4MB is used for buffers that contain data that has yet to be flushed to disk. ~627MB is used for the disk cache that contains data that has been read off the disk in the past.

<a name="ch03ex02"></a>

##### Listing 3.2\.

<pre>bash-2.05b$ vmstat

procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   <span class="docEmphStrong">swpd   free   buff  cache   si   so</span>     bi   bo   in    cs us sy id wa

 0  0 <span class="docEmphStrong">511012  14840   4412 642072   33   31</span>    204  247 1110  1548  8  5 73 14

</pre>

In [Listing 3.3](ch03lev1sec2.html#ch03ex03), we ask vmstat to display information about the number of active and inactive pages. The amount of inactive pages indicates how much of the memory could be swapped to disk and how much is currently being used. In this case, we can see that 1310MB of memory is active, and only 78MB is considered inactive. This machine has a large amount of memory, and much of it is <a name="iddle0504"></a><a name="iddle0505"></a><a name="iddle0506"></a><a name="iddle0507"></a><a name="iddle0508"></a><a name="iddle0509"></a><a name="iddle0510"></a>being actively used.

<a name="ch03ex03"></a>

##### Listing 3.3\.

<pre>bash-2.05b$ vmstat -a

procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   swpd   free  <span class="docEmphStrong">inact active</span>   si   so    bi    bo   in    cs us sy id wa

 2  1 514004   5640 <span class="docEmphStrong">79816 1341208</span>   33   31   204   247 1111  1548  8  5 73 14

</pre>

Next, in [Listing 3.4](ch03lev1sec2.html#ch03ex04), we look at a different system, one that is actively swapping data in and out of memory. The <tt>si</tt> column <a name="iddle0511"></a><a name="iddle0512"></a><a name="iddle0513"></a>indicates that swap data has been read in at a rate of 480KB, 832KB, 764KB, 344KB, and 512KB during each of those sample periods. The <tt>so</tt> column indicates that memory data has been written to swap at a rate of 9KB, 0KB, 916KB, 0KB, 1068KB, 444KB, 792KB, during each of the samples. These results could indicate that the system does not have enough memory to handle all the running processes. A simultaneously high swap-in and swap-out rate can occur when a process's memory is being saved to make way for an application that had been previously swapped to disk. This can be disastrous if two running programs both need more memory than the system can provide. For example, if two processes are using a large amount of memory, and both are trying to run simultaneously, each can cause the other's memory to be written to swap. When one of the programs needs a piece of memory, it kicks out one that the other applications needs. When the other application starts to run, it kicks out a piece of memory that the original program was using, and waits until its memory is loaded from the swap. This can cause both applications to grind to a halt while they wait for their memory to be retrieved from swap before they can continue execution. As soon as one makes a little bit of progress, it swaps out memory that the other process was using and causes the other program to slow down. This is called thrashing. <a name="iddle0514"></a><a name="iddle0515"></a>When this happens, the system spends most of its time reading memory to and from the swap, and system performance dramatically slows down.

In this particular case, the swapping eventually stopped, so most likely the memory that was swapped to disk was not immediately needed by the original process. This means the swap usage was effective, the contents of the memory that was not being used was written to disk, and the memory was then given to <a name="iddle0516"></a><a name="iddle0517"></a><a name="iddle0518"></a><a name="iddle0519"></a><a name="iddle0520"></a><a name="iddle0521"></a>the process that needed it.

<a name="ch03ex04"></a>

##### Listing 3.4\.

<pre>[ezolt@localhost book]$ vmstat 1 100

procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   swpd   free   buff  cache   <span class="docEmphStrong">si   so</span>    bi    bo   in    cs us sy id wa

 2  1 131560   2320   8640  53036    <span class="docEmphStrong">1    9</span>   107    69 1137   426 10  7 74  9

 0  1 131560   2244   8640  53076  <span class="docEmphStrong">480    0</span>   716     0 1048   207  6  1  0 93

 1  2 132476   3424   8592  53272  <span class="docEmphStrong">832  916</span>  1356   916 1259   692 11  4  0 85

 1  0 132476   2400   8600  53280  <span class="docEmphStrong">764    0</span>  1040    40 1288   762 14  5  0 81

 0  1 133544   2656   8624  53392  <span class="docEmphStrong">344 1068</span>  1096  1068 1217   436  8  3  5 84

 0  1 133988   2300   8620  54288  <span class="docEmphStrong">512  444</span>  1796   444 1090   230  5  1  2 92

 0  0 134780   3148   8612  53688    <span class="docEmphStrong">0  792</span>     0   792 1040   166  5  1 92  2

 0  0 134780   3148   8612  53688    <span class="docEmphStrong">0    0</span>     0     0 1050   158  4  1 95  0

 0  0 134780   3148   8612  53688    <span class="docEmphStrong">0    0</span>     0     0 1148   451  7  2 91  0

 0  0 134780   3148   8620  53680    <span class="docEmphStrong">0    0</span>     0    12 1196   477  8  2 78 12

 ....

</pre>

As shown in [Listing 3.5](ch03lev1sec2.html#ch03ex05), as you saw in the previous chapter, vmstat can show a vast array of different system statistics. Now as we look at it, we can see some of the same statistics that were present in some of the other output modes, such as active, inactive, buffer, cache, and used swap. However, it also has a few new statistics, such as total memory, which indicates that this system has a total of 1516MB of memory, and total swap, which indicates that this system has a total of 2048MB of swap. It can be helpful to know the system totals when trying to figure out what percentage of the swap and memory is currently being used. Another interesting statistic is the pages paged in, which indicates the total number of pages that were read from the disk. This statistic includes the pages that are read starting an application and those that the application itself may be <a name="iddle0522"></a><a name="iddle0523"></a><a name="iddle0524"></a>using.

<a name="ch03ex05"></a>

##### Listing 3.5\.

<pre>

bash-2.05b$ vmstat -s

      <span class="docEmphStrong">1552528  total memory

      1546692  used memory

      1410448  active memory

        11100  inactive memory

         5836  free memory

         2676  buffer memory

       645864  swap cache

      2097096  total swap

       526280  used swap

      1570816  free swap</span>

     20293225 non-nice user cpu ticks

     18284715 nice user cpu ticks

     17687435 system cpu ticks

    357314699 idle cpu ticks

     67673539 IO-wait cpu ticks

       352225 IRQ cpu ticks

      4872449 softirq cpu ticks

    <span class="docEmphStrong">495248623 pages paged in

    600129070 pages paged out

     19877382 pages swapped in

     18874460 pages swapped out</span>

   2702803833 interrupts

   3763550322 CPU context switches

   1094067854 boot time

     20158151 forks

</pre>

Finally, in [Listing 3.6](ch03lev1sec2.html#ch03ex06), we see that vmstat can provide information about how the Linux kernel <a name="iddle0525"></a><a name="iddle0526"></a><a name="iddle0527"></a><a name="iddle0528"></a>allocates its memory. As previously described, the Linux kernel has a series of "slabs" to hold its dynamic data structures. vmstat displays each of the slabs (Cache), shows how many of the elements are being used (Num), shows how many are allocated (Total), shows the size of each element (Size), and shows the amount of memory in pages (Pages) that the total slab is using. This can be helpful when tracking down exactly how the kernel is using its <a name="iddle0529"></a><a name="iddle0530"></a><a name="iddle0531"></a>memory.

<a name="ch03ex06"></a>

##### Listing 3.6\.

<pre>

bash-2.05b$ vmstat -m

Cache                          Num   Total   Size   Pages

udf_inode_cache                  0       0    416       9

fib6_nodes                       7     113     32     113

ip6_dst_cache                    9      17    224      17

ndisc_cache                      1      24    160      24

raw6_sock                        0       0    672       6

udp6_sock                        0       0    640       6

tcp6_sock                      404     441   1120       7

ip_fib_hash                     39     202     16     202

ext3_inode_cache              1714    3632    512       8

...

</pre>

<tt>vmstat</tt> provides an easy way to extract large amounts of information about the Linux memory <a name="iddle0532"></a><a name="iddle0533"></a><a name="iddle0534"></a><a name="iddle0535"></a>subsystem. When combined with the other information provided on the default output screen, it provides a fair picture of the health and resource usage of the system.

<a name="ch03lev2sec4"></a>

#### 3.2.2\. top (2.x and 3.x)

As discussed in the previous chapter, <tt>top</tt> presents both system-wide and process-specific performance statistics. By default, <tt>top</tt> presents a list, in decreasing order, of the top CPU-consuming processes, but it can also be adjusted to sort by the total memory usage, enabling you to track down which process is using the most memory.

<a name="ch03lev3sec8"></a>

##### 3.2.2.1 Memory Performance-Related Options

<tt>top</tt> does not have any <a name="iddle0536"></a><a name="iddle0537"></a><a name="iddle0538"></a>special command-line options that manipulate its display of memory statistics. It is invoked with the following command line:

<pre>top

</pre>

However, once running, <tt>top</tt> enables you to select whether system-wide memory information displays, and whether processes are sorted by memory usage. Sorting by memory consumption proves particularly useful to determine which process is consuming the most memory. [Table 3-3](ch03lev1sec2.html#ch03table03) describes the different memory-related output toggles.

<a name="ch03table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-3\. <span class="docEmphasis"><tt>top</tt></span> Runtime Toggles

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0539"></a><a name="iddle0540"></a><a name="iddle0541"></a><a name="iddle0542"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>m</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0543"></a>This toggles whether information about the system memory usage will be shown on the screen.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>M</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0544"></a>Sorts the tasks by the amount of memory they are using. Because processes may have allocated more memory than they are using, this sorts by resident set size. Resident set size is the amount the processes are actually using rather than what they have simply asked for.<a name="iddle0545"></a><a name="iddle0546"></a><a name="iddle0547"></a><a name="iddle0548"></a>

</td>

</tr>

</tbody>

</table>

[Table 3-4](ch03lev1sec2.html#ch03table04) describes <a name="iddle0549"></a><a name="iddle0550"></a><a name="iddle0551"></a>the memory performance statistics that <tt>top</tt> can provide for both the entire system and individual processes. <tt>top</tt> has two different versions, 2.x and 3.x, which have slightly different names for output statistics. [Table 3-4](ch03lev1sec2.html#ch03table04) describes the names for both versions.

<a name="ch03table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-4\. <span class="docEmphasis"><tt>top</tt></span> Memory Performance Statistics

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

<tt>%MEM</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0552"></a>This is the percentage of the system's physical memory that this process is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SIZE (v 2.x)</tt>

<tt>VIRT (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0553"></a>This is the total size of the process's virtual memory usage. This includes all the memory that the application has allocated but is not using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SWAP</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0554"></a>This is the amount of swap (in KB) that the process is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>RSS (v 2.x)</tt>

<tt>RES (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0555"></a>This is the amount of physical memory that the application is actually using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>TRS (v 2.x)</tt>

<tt>CODE (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0556"></a>The total amount of physical memory (in KB) that the process's executable code is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>DSIZE (v 2.x)</tt>

<tt>DATA (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0557"></a>The total amount of memory (in KB) dedicated to a process's data and stack.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SHARE (v 2.x)</tt>

<tt>SHR (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0558"></a>The total amount of memory (in KB) that can be shared with other processors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>D (v 2.x)</tt>

<tt>nDRT (v 3.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0559"></a>The number of pages that are dirty and need to be flushed to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Mem:</tt>

<tt>total, used, free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0560"></a>Of the physical memory, this indicates the total amount, the used amount, and the free amount.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>swap: total, used, free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0561"></a>Of the swap, this indicates the total amount, the used amount, and the free amount.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>active (v 2.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0562"></a>The amount of physical memory currently active.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>inactive (v 2.x)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0563"></a>The amount of physical memory that is inactive and hasn't been used in a while.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>buffers</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0564"></a>The total amount of physical memory (in KB) used to buffer values to be written to disk.

</td>

</tr>

</tbody>

</table>

<tt>top</tt> provides a large amount of memory information about the different running processes. As discussed in later chapters, you can use this information to determine exactly how an application allocates and uses <a name="iddle0565"></a><a name="iddle0566"></a><a name="iddle0567"></a>memory.

<a name="ch03lev3sec9"></a>

##### 3.2.2.2 Example Usage

[Listing 3.7](ch03lev1sec2.html#ch03ex07) is similar <a name="iddle0568"></a><a name="iddle0569"></a><a name="iddle0570"></a>to the example run of <tt>top</tt> shown in the previous chapter. However, in this example, notice that in the buffers, we have a total amount of 1,024MB of physical memory, of which ~84MB is free.

<a name="ch03ex07"></a>

##### Listing 3.7\.

<pre>[ezolt@wintermute doc]$ top

top - 15:47:03 up 24 days,  4:32, 15 users,  load average: 1.17, 1.19, 1.17

Tasks: 151 total,   1 running, 138 sleeping,  11 stopped,   1 zombie

Cpu(s):  1.2% us,  0.7% sy,  0.0% ni, 93.0% id,  4.9% wa,  0.0% hi,  0.1% si

Mem:   1034320k total,   948336k used,    85984k free,    32840k buffers

Swap:  2040244k total,   276796k used,  1763448k free,   460864k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND

26364 root      16   0  405m  71m 321m S  4.0  7.1 462:25.50 X

17345 ezolt     16   0  176m  73m  98m S  2.6  7.3   1:17.48 soffice.bin

18316 ezolt     16   0  2756 1096 1784 R  0.7  0.1   0:05.54 top

26429 ezolt     16   0 65588  52m  12m S  0.3  5.2  16:16.77 metacity

26510 ezolt     16   0 19728 5660  16m S  0.3  0.5  27:57.87 clock-applet

26737 ezolt     16   0 70224  35m  20m S  0.3  3.5   8:32.28 gnome-terminal

     1 root     16   0  2396  448 1316 S  0.0  0.0   0:01.72 init

     2 root     RT   0     0    0    0 S  0.0  0.0   0:00.88 migration/0

     3 root     34  19     0    0    0 S  0.0  0.0   0:00.01 ksoftirqd/0

     4 root     RT   0     0    0    0 S  0.0  0.0   0:00.35 migration/1

     5 root     34  19     0    0    0 S  0.0  0.0   0:00.01 ksoftirqd/1

     6 root     RT   0     0    0    0 S  0.0  0.0   0:34.20 migration/2

     7 root     34  19     0    0    0 S  0.0  0.0   0:00.01 ksoftirqd/2

</pre>

Again, top can be customized to display <a name="iddle0571"></a><a name="iddle0572"></a><a name="iddle0573"></a>only what you are interested in observing. [Listing 3.8](ch03lev1sec2.html#ch03ex08) shows a highly configured output screen that shows only memory performance statistics.

<a name="ch03ex08"></a>

##### Listing 3.8\.

<pre>Mem:   1034320k total,   948336k used,    85984k free,    33024k buffers

Swap:  2040244k total,   276796k used,  1763448k free,   460680k cached

 VIRT  RES  SHR %MEM SWAP CODE DATA nFLT nDRT COMMAND

 405m  71m 321m  7.1 333m 1696 403m 4328    0 X

70224  35m  20m  3.5  33m  280  68m 3898    0 gnome-terminal

 2756 1104 1784  0.1 1652   52 2704    0    0 top

19728 5660  16m  0.5  13m   44  19m   17    0 clock-applet

 2396  448 1316  0.0 1948   36 2360   16    0 init

    0    0    0  0.0    0    0    0    0    0 migration/0

    0    0    0  0.0    0    0    0    0    0 ksoftirqd/0

    0    0    0  0.0    0    0    0    0    0 migration/1

    0    0    0  0.0    0    0    0    0    0 ksoftirqd/1

    0    0    0  0.0    0    0    0    0    0 migration/2

    0    0    0  0.0    0    0    0    0    0 ksoftirqd/2

    0    0    0  0.0    0    0    0    0    0 migration/3

</pre>

<tt>top</tt> provides a real-time update of memory statistics and a display of which processes are using which types of memory. This information becomes useful as we investigate application memory <a name="iddle0574"></a><a name="iddle0575"></a><a name="iddle0576"></a>usage.

<a name="ch03lev2sec5"></a>

#### 3.2.3\. procinfo II

As we've seen before, <tt>procinfo</tt> provides a view of the system-wide performance characteristics. In addition to the statistics described in the previous chapter, <tt>procinfo</tt> provides a few memory statistics, similar to <tt>vmstat</tt> and <tt>top</tt>, that indicate how the current memory is being used.

<a name="ch03lev3sec10"></a>

##### 3.2.3.1 Memory Performance-Related Options

<tt>procinfo</tt> does not <a name="iddle0577"></a><a name="iddle0578"></a><a name="iddle0579"></a>have any options that change the output of the memory statistics displayed and, as a result, is invoked with the following command:

<pre>procinfo

</pre>

<tt>procinfo</tt> displays the basic memory system memory statistics, similar to top and <tt>vmstat</tt>. These are shown in [Table 3-5](ch03lev1sec2.html#ch03table05).

<a name="ch03table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-5\. <span class="docEmphasis"><tt>procinfo</tt></span> CPU Statistics

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0580"></a><a name="iddle0581"></a><a name="iddle0582"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Total</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0583"></a>This is the total amount of physical memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Used</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0584"></a>This is the amount of physical memory in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0585"></a>This is the amount of unused physical memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Shared</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0586"></a>This is an obsolete value and should be ignored.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Buffers</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0587"></a>This is the amount of physical memory used as buffers for disk writes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Page in</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0588"></a>The number of blocks (usually 1KB) read from disk. (This is broken on 2.6.x kernels.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Page out</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0589"></a>The number of blocks (usually 1KB) written to disk. (This is broken on 2.6.x kernels.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Swap in</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0590"></a>The number of memory pages read in from swap. (This statistic is broken on 2.6.x kernels.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Swap out</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0591"></a>The number of memory pages written to swap. (This statistic is broken on 2.6.x kernels.)

</td>

</tr>

</tbody>

</table>

Much like <tt>vmstat</tt> or <tt>top</tt>, <tt>procinfo</tt> is a low-overhead command that is good to leave running in a console or window on the screen. It gives a good indication of a system's health and <a name="iddle0592"></a><a name="iddle0593"></a><a name="iddle0594"></a>performance.

<a name="ch03lev3sec11"></a>

##### 3.2.3.2 Example Usage

[Listing 3.9](ch03lev1sec2.html#ch03ex09) is a <a name="iddle0595"></a><a name="iddle0596"></a><a name="iddle0597"></a>typical output for <tt>procinfo</tt>. As you can see, it reports summary information about how the system is using virtual memory. In this case, the system has a total of 312MB of memory; 301MB is in use by the kernel and applications, 11MB is used by system buffers, and 11MB is not used at all.

<a name="ch03ex09"></a>

##### Listing 3.9\.

<pre>[ezolt@localhost procinfo-18]$ ./procinfo

Linux 2.6.6-1.435.2.3smp (bhcompile@tweety.build.redhat.com) (gcc 3.3.3 20040412 )

#1

1CPU [localhost]

<span class="docEmphStrong">Memory:      Total        Used        Free      Shared      Buffers

Mem:        320468      308776       11692           0        11604

Swap:       655192      220696      434496</span>

Bootup: Sun Oct 24 10:03:43 2004    Load average: 0.44 0.53 0.51 3/110 32243

user  :       0:57:58.92   9.0%  page in :        0

nice  :       0:02:51.09   0.4%  page out:        0

system:       0:20:18.43   3.2%  swap in :        0

idle  :       8:47:31.54  81.9%  swap out:        0

uptime:      10:44:01.94         context : 13368094

irq  0:  38645994 timer                 irq  7:         2

irq  1:     90516 i8042                 irq  8:         1 rtc

irq  2:         0 cascade [4]           irq  9:         2

irq  3:    742857 prism2_cs             irq 10:         2

irq  4:         6                       irq 11:    562551 uhci_hcd, yenta, yen

irq  5:         2                       irq 12:   1000803 i8042

irq  6:         8                       irq 14:    207681 ide0

</pre>

<tt>procinfo</tt> provides information about system performance in a single screen of information. Although it provides a few of the important statistics for memory, <tt>vmstat</tt> or <tt>top</tt> is much better suited for investigating system-wide <a name="iddle0598"></a><a name="iddle0599"></a><a name="iddle0600"></a>memory usage.

<a name="ch03lev2sec6"></a>

#### 3.2.4\. gnome-system-monitor (II)

<tt>gnome-system-monitor</tt> is in many ways a graphical counterpart of <tt>top</tt>. It enables you to monitor individual process and observe the load on the system based on the graphs that it displays. It also provides rudimentary graphs of CPU and memory usage.

<a name="ch03lev3sec12"></a>

##### 3.2.4.1 Memory Performance-Related Options

<tt>gnome-system-monitor</tt> can be <a name="iddle0601"></a><a name="iddle0602"></a><a name="iddle0603"></a>invoked from the Gnome menu. (Under Red Hat 9 and higher, this is in System Tools > System Monitor.) However, it can also be invoked using the following command:

<pre>gnome-system-monitor

</pre>

<tt>gnome-system-monitor</tt> has no relevant command-line options that affect the memory performance <a name="iddle0604"></a><a name="iddle0605"></a><a name="iddle0606"></a>measurements.

<a name="ch03lev3sec13"></a>

##### 3.2.4.2 Example Usage

When you <a name="iddle0607"></a><a name="iddle0608"></a><a name="iddle0609"></a>launch <tt>gnome-system-monitor</tt> and select the System Monitor tab, you see a window similar to [Figure 3-1](ch03lev1sec2.html#ch03fig01). This window enables you to glance at the graph and see how much physical memory and swap is currently being used, and how its usage has changed over time. In this case, we see that 969MB of a total of 1,007MB is currently being used. The memory usage has been relatively flat for a while.

<a name="ch03fig01"></a>

<center>

##### Figure 3-1\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/03fig01.jpg)

</center>

The graphical view of data provided by <tt>gnome-system-monitor</tt> can make it easier and faster; however, most of the details, such as how the memory is <a name="iddle0610"></a><a name="iddle0611"></a><a name="iddle0612"></a>being used, are missing.

<a name="ch03lev2sec7"></a>

#### 3.2.5\. free

<tt>free</tt> provides an <a name="iddle0613"></a><a name="iddle0614"></a><a name="iddle0615"></a>overall view of how your system is using your memory, including the amount of free memory. Although the <tt>free</tt> command may show that a particular system does not have much free memory, this is not necessarily bad. Instead of letting memory sit unused, the Linux kernel puts it to work as a cache for disk reads and as a buffer for disk writes. This can dramatically increase system performance. Because these cache and buffers can always be discarded and the memory can be used if needed by applications, <tt>free</tt> shows you the amount of free memory plus or minus these buffers.

<a name="ch03lev3sec14"></a>

##### 3.2.5.1 Memory Performance-Related Options

<tt>free</tt> can be invoked using the following <a name="iddle0616"></a><a name="iddle0617"></a><a name="iddle0618"></a>command line:

<pre>free [-l] [-t] [-s delay ] [-c count ]

</pre>

[Table 3-6](ch03lev1sec2.html#ch03table06) describes the parameters that modify the types of statistics that free displays. Much like <a name="iddle0619"></a><a name="iddle0620"></a><a name="iddle0621"></a><a name="iddle0622"></a><tt>vmstat</tt>, <tt>free</tt> can periodically display updated memory statistics.

<a name="ch03table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-6\. <span class="docEmphasis"><tt>free</tt></span> Command-Line Options

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

<tt>-s delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0623"></a>This option causes <tt>free</tt> to print out new memory statistics every <tt>delay</tt> seconds.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-c count</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0624"></a>This option causes <tt>free</tt> to print out new statistics for <tt>count</tt> times.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-l</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0625"></a>This option shows you how much high memory and how much low memory are being used.

</td>

</tr>

</tbody>

</table>

<tt>free</tt> actually displays some of the most complete memory statistics of any of the memory statistic tools. The statistics that it displays are shown <a name="iddle0626"></a><a name="iddle0627"></a><a name="iddle0628"></a><a name="iddle0629"></a>in [Table 3-7](ch03lev1sec2.html#ch03table07).

<a name="ch03table07"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-7\. <span class="docEmphasis"><tt>free</tt></span> Memory Statistics

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0630"></a><a name="iddle0631"></a><a name="iddle0632"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Total</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0633"></a>This is the total amount of physical memory and swap.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Used</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0634"></a>This is the amount of physical memory and swap in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0635"></a>This is the amount of unused physical memory and swap.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Shared</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0636"></a>This is an obsolete value and should be ignored.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Buffers</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0637"></a>This is the amount of physical memory used as buffers for disk writes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Cached</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0638"></a>This is the amount of physical memory used as cache for disk reads.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-/+ buffers/cache</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0639"></a>In the <tt>Used</tt> column, this shows the amount of memory that would be used if buffers/cache were not counted as used memory. In the <tt>Free</tt> column, this shows the amount of memory that would be free if buffers/cache were counted as free memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Low</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0640"></a>The total amount of low memory or memory directly accessible by the kernel.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>High</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0641"></a>The total amount of high memory or memory not directly accessible by the kernel.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Totals</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0642"></a>This shows the combination of physical memory and swap for the <tt>Total</tt>, <tt>Used</tt>, and <tt>Free</tt> columns.

</td>

</tr>

</tbody>

</table>

<tt>free</tt> provides information about the system-wide memory usage of Linux. It is a fairly complete range of memory <a name="iddle0643"></a><a name="iddle0644"></a><a name="iddle0645"></a>statistics.

<a name="ch03lev3sec15"></a>

##### 3.2.5.2 Example Usage

Calling <tt>free</tt> without any <a name="iddle0646"></a><a name="iddle0647"></a><a name="iddle0648"></a>command options gives you an overall view of the memory subsystem.

As mentioned previously, Linux tries to use all the available memory if possible to cache data and applications. In [Listing 3.10](ch03lev1sec2.html#ch03ex10), <tt>free</tt> tells us that we are currently using 234,720 bytes of memory; however, if you ignore the buffers and cache, we are only using 122,772 bytes of memory. The opposite is true of the <tt>free</tt> column. We currently have 150,428 bytes of memory free; if you also count the buffers and cached memory (which you can, because Linux throws away those buffers if the memory is needed), however, we have 262,376 bytes <a name="iddle0649"></a><a name="iddle0650"></a><a name="iddle0651"></a>of memory free.

<a name="ch03ex10"></a>

##### Listing 3.10\.

<pre>

[ezolt@wintermute procps-3.2.0]$ free

             total       used       free     shared    buffers      cached

Mem:        385148     234720     150428          0       8016      103932

-/+ buffers/cache:     122772     262376

Swap:       394080      81756     312324

</pre>

Although you could just total the columns yourself, the <tt>-t</tt> flag shown in [Listing 3.11](ch03lev1sec2.html#ch03ex11) tells you the totals when adding both swap and real memory. In this case, the system had 376MB of physical memory and 384MB of swap. The total amount of memory available on the system is 376MB plus 384MB, or ~760MB. The total amount of free memory was 134MB of physical memory plus 259MB of swap, yielding a total of 393MB of free <a name="iddle0652"></a><a name="iddle0653"></a><a name="iddle0654"></a>memory.

<a name="ch03ex11"></a>

##### Listing 3.11\.

<pre>[ezolt@wintermute procps-3.2.0]$ free -t

             total       used       free     shared    buffers      cached

Mem:        385148     247088     138060          0       9052      115024

-/+ buffers/cache:     123012     262136

Swap:       394080      81756     312324

Total:      779228     328844     450384

</pre>

Finally, <tt>free</tt> tells you the amount of high and low memory that the system is using. This is mainly useful on 32-bit machines (such as IA32) with 1GB or more of physical memory. (32-bit machines are the only machines that will have high memory.) [Listing 3.12](ch03lev1sec2.html#ch03ex12) shows a system with a very small amount of free memory, 6MB in total. It shows a system with 876MB of low memory and 640MB of high memory. This system also has much more cached memory than buffer memory, suggesting that it may be aggressively writing data to disk rather than leaving it in the buffer cache a long time.

<a name="ch03ex12"></a>

##### Listing 3.12\.

<pre>

fas% free -l

             total       used       free     shared    buffers      cached

Mem:       1552528    1546472       6056          0       7544      701408

Low:        897192     892800       4392

High:       655336     653672       1664

-/+ buffers/cache:     837520     715008

Swap:      2097096     566316    1530780

</pre>

<tt>free</tt> gives a good idea of how the system memory is being used. It may take a little while to get used to output format, but it contains all the important <a name="iddle0655"></a><a name="iddle0656"></a><a name="iddle0657"></a>memory statistics.

<a name="ch03lev2sec8"></a>

#### 3.2.6\. slabtop

<tt>slabtop</tt> is similar to <tt>top</tt>, but instead of displaying information about the CPU and memory usage of the processes in the system, <tt>slabtop</tt> shows in real-time how the kernel is allocating its various caches and how full they are. Internally, the kernel has a series of caches that are made up of one or more slabs. Each slab consists of a set of one or more objects. These objects can be active (or used) or inactive (unused). <tt>slabtop</tt> shows you the status of the different slabs. It shows you how full they are and how much memory they are using.

<a name="ch03lev3sec16"></a>

##### 3.2.6.1 Memory Performance-Related Options

<tt>slabtop</tt> is invoked <a name="iddle0658"></a><a name="iddle0659"></a><a name="iddle0660"></a>using the following command line:

<pre>slabtop [--delay n –sort={a | b | c | l | v | n | o | p | s | u}

</pre>

The command-line options for slabtop are described in [Table 3-8](ch03lev1sec2.html#ch03table08).

<a name="ch03table08"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-8\. <span class="docEmphasis"><tt>slabtop</tt></span> Command-Line Options

</caption><colgroup><col width="200"><col width="100"><col width="200"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0661"></a><a name="iddle0662"></a><a name="iddle0663"></a><a name="iddle0664"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--delay</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="3">

<a name="iddle0665"></a>This specifies how long <tt>slabtop</tt> waits between updates.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--sort {order}</tt>

</td>

<td class="docTableCell" align="left" valign="top" colspan="3">

<a name="iddle0666"></a>This specifies the order of the output. <tt>order</tt> can be one of the following:

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>a</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0667"></a>This sorts by the number of active objects in each slab.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>b</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0668"></a>This sorts by the total number of objects (active and inactive) in each slab for a particular cache.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>c</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0669"></a>This sorts by the total amount of memory each cache is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>l</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0670"></a>This sorts by the number of slabs used by each cache.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>v</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0671"></a>This sorts by the number of active slabs used by each cache.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>n</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0672"></a>This sorts by the name of the cache.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>o</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0673"></a>This sorts by the number of objects in the particular cache.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>P</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0674"></a>This sorts by the number of pages used per slab.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0675"></a>This sorts by the size of the objects in the cache.

</td>

</tr>

</tbody>

</table>

<tt>slabtop</tt> provides a glimpse into the data structures of the Linux kernel. Each of these slab types is tied closed to the Linux kernel, and a description of each of these slabs is beyond the scope of this book. If a particular slab is using a large amount of kernel memory, reading the Linux kernel source code and searching the Web are two great ways to figure out what these slabs are used <a name="iddle0676"></a><a name="iddle0677"></a><a name="iddle0678"></a><a name="iddle0679"></a>for.

<a name="ch03lev3sec17"></a>

##### 3.2.6.2 Example Usage

As shown in <a name="iddle0680"></a><a name="iddle0681"></a><a name="iddle0682"></a>[Listing 3.13](ch03lev1sec2.html#ch03ex13), by default, <tt>slabtop</tt> fills the entire console and continually updates the statistics every three seconds. In this example, you can see that the size-64 slab has the most objects, only half of which are active.

<a name="ch03ex13"></a>

##### Listing 3.13\.

<pre>[ezolt@wintermute proc]$ slabtop

 Active / Total Objects (% used)    : 185642 / 242415 (76.6%)

 Active / Total Slabs (% used)      : 12586 / 12597 (99.9%)

 Active / Total Caches (% used)     : 88 / 134 (65.7%)

 Active / Total Size (% used)       : 42826.23K / 50334.67K (85.1%)

 Minimum / Average / Maximum Object : 0.01K / 0.21K / 128.00K

  OBJS ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME

 66124  34395  52%    0.06K   1084       61      4336K size-64

 38700  35699  92%    0.05K    516       75      2064K buffer_head

 30992  30046  96%    0.15K   1192       26      4768K dentry_cache

 21910  21867  99%    0.27K   1565       14      6260K radix_tree_node

 20648  20626  99%    0.50K   2581        8     10324K ext3_inode_cache

 11781   7430  63%    0.03K     99      119       396K size-32

  9675   8356  86%    0.09K    215       45       860K vm_area_struct

  6024   2064  34%    0.62K   1004        6      4016K ntfs_big_inode_cache

  4520   3633  80%    0.02K     20      226        80K anon_vma

  4515   3891  86%    0.25K    301       15      1204K filp

  4464   1648  36%    0.12K    144       31       576K size-128

  3010   3010 100%    0.38K    301       10      1204K proc_inode_cache

  2344    587  25%    0.50K    293        8      1172K size-512

  2250   2204  97%    0.38K    225       10       900K inode_cache

  2100    699  33%    0.25K    140       15       560K size-256

  1692   1687  99%    0.62K    282        6      1128K nfs_inode_cache

  1141   1141 100%    4.00K   1141        1      4564K size-4096

</pre>

Because the information provided by <tt>slabtop</tt> is updated periodically, it is a great way to see how the Linux kernel's memory usage changes in response <a name="iddle0683"></a><a name="iddle0684"></a><a name="iddle0685"></a>to different workloads.

<a name="ch03lev2sec9"></a>

#### 3.2.7\. sar (II)

All the advantages of using <tt>sar</tt> <a name="iddle0686"></a><a name="iddle0687"></a><a name="iddle0688"></a>as a CPU performance tool, such as the easy recording of samples, extraction to multiple output formats, and time stamping of each sample, are still present when monitoring memory statistics. <tt>sar</tt> provides similar information to the other memory statistics tools, such as the current values for the amount of free memory, buffers, cached, and swap amount. However, it also provides the rate at which these value change and provides information about the percentage of physical memory and swap that is currently being consumed.

<a name="ch03lev3sec18"></a>

##### 3.2.7.1 Memory Performance-Related Options

<tt>sar</tt> can be invoked with the following command line:

<pre>sar [-B] [-r] [-R]

</pre>

By default, sar displays only CPU performance statistics; so to retrieve any of the memory subsystem statistics, you must use the options described in <a name="iddle0689"></a><a name="iddle0690"></a><a name="iddle0691"></a>[Table 3-9](ch03lev1sec2.html#ch03table09).

<a name="ch03table09"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-9\. <span class="docEmphasis"><tt>sar</tt></span> Command-Line Options

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0692"></a><a name="iddle0693"></a><a name="iddle0694"></a><a name="iddle0695"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-B</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0696"></a>This reports information about the number of blocks that the kernel swapped to and from disk. In addition, for kernel versions after v2.5, it reports information about the number of page faults.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-W</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0697"></a>This reports the number of pages of swap that are brought in and out of the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-r</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0698"></a>This reports information about the memory being used in the system. It includes information about the total free memory, swap, cache, and buffers being used.

</td>

</tr>

</tbody>

</table>

<tt>sar</tt> provides a fairly complete view of the Linux memory subsystem. One advantage that <tt>sar</tt> provides over other tools is that it shows the rate of change for many of the important values in addition to the absolute values. You can use these values to see exactly how memory usage is changing over time without having to figure out the differences between values at each sample. [Table 3-10](ch03lev1sec2.html#ch03table10) shows the memory statistics that <tt>sar</tt> <a name="iddle0699"></a><a name="iddle0700"></a><a name="iddle0701"></a>provides.

<a name="ch03table10"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-10\. <span class="docEmphasis"><tt>sar</tt></span> Memory Statistics

</caption><colgroup><col width="200"><col width="300"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pgpgin/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0702"></a>The amount of memory (in KB) that the kernel paged in from disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pgpgout/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0703"></a>The amount of memory (in KB) that the kernel paged out to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>fault/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0704"></a>The total number of faults that that the memory subsystem needed to fill. These may or may not have required a disk access.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>majflt/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0705"></a>The total number of faults that the memory subsystem needed to fill and required a disk access.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pswpin/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0706"></a>The amount of swap (in pages) that the system brought into memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pswpout/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0707"></a>The amount of memory (in pages) that the system wrote to swap.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbmemfree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0708"></a>This is the total physical memory (in KB) that is currently free or not being used.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbmemused</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0709"></a>This is the total amount of physical memory (in KB) currently being used.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>%memused</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0710"></a>This is the percentage of the total physical memory being used.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbbuffers</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0711"></a>This is the amount of physical memory used as buffers for disk writes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbcached</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0712"></a>This is the amount of physical memory used as cache for disk reads.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbswpfree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0713"></a>This is the amount of swap (in KB) currently free.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbswpused</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0714"></a>This is the amount of swap (in KB) currently used.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>%swpused</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0715"></a>This is the percentage of the swap being used.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>kbswpcad</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0716"></a>This is memory that is both swapped to disk and present in memory. If the memory is needed, it can be immediately reused because the data is already present in the swap area.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>frmpg/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0717"></a>The rate that the system is freeing memory pages. A negative number means the system is allocating them.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>bufpg/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0718"></a>The rate that the system is using new memory pages as buffers. A negative number means that number of buffers is shrinking, and the system is using less of them.

</td>

</tr>

</tbody>

</table>

Although <tt>sar</tt> misses the high and low memory statistics, it provides nearly every other memory statistic. The fact that it can also record network CPU and disk I/O statistics makes it very <a name="iddle0719"></a><a name="iddle0720"></a><a name="iddle0721"></a>powerful.

<a name="ch03lev3sec19"></a>

##### 3.2.7.2 Example Usage

[Listing 3.14](ch03lev1sec2.html#ch03ex14) shows <tt>sar</tt> <a name="iddle0722"></a><a name="iddle0723"></a><a name="iddle0724"></a>providing information about the current state of the memory subsystem. From the results, we can see that the amount of memory that the system used varies from 98.87 percent to 99.25 percent of the total memory. Over the course of the observation, the amount of free memory drops from 11MB to 7MB. The percentage of swap that is used hovers around ~11 percent. The system has ~266MB of data cache and about 12MB in buffers that can be written to disk.

<a name="ch03ex14"></a>

##### Listing 3.14\.

<a name="PLID19"></a>

<pre>

[ezolt@scrffy manuscript]$ sar -r 1 5

Linux 2.6.8-1.521smp (scrffy)   10/25/2004

09:45:30 AM kbmemfree kbmemused  %memused kbbuffers  kbcached kbswpfree kbswpused  

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif)%swpused  kbswpcad

09:45:31 AM     11732   1022588     98.87     12636    272284   1816140    224104     10

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).98     66080

09:45:32 AM     10068   1024252     99.03     12660    273300   1816140    224104     10

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).98     66080

09:45:33 AM      5348   1028972     99.48     12748    275292   1816140    224104     10

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).98     66080

09:45:35 AM      4932   1029388     99.52     12732    273748   1816140    224104     10

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).98     66080

09:45:36 AM      6968   1027352     99.33     12724    271876   1815560    224684     11

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).01     66660

Average:         7810   1026510     99.25     12700    273300   1816024    224220     10

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif).99     66196

</pre>

[Listing 3.15](ch03lev1sec2.html#ch03ex15) shows that the system is consuming the free memory at a rate of ~82 pages per second during the first sample. Later, it frees ~16 pages, and then consumes ~20 pages. The number pages of buffers grew only once during the observation, at a rate of 2.02 pages per second. Finally, the pages of cache <a name="iddle0725"></a><a name="iddle0726"></a><a name="iddle0727"></a>shrunk by 2.02, but in the end, they expanded by 64.36 pages/second.

<a name="ch03ex15"></a>

##### Listing 3.15\.

<pre>[ezolt@scrffy manuscript]$ sar -R 1 5

Linux 2.6.8-1.521smp (scrffy)   10/25/2004

09:57:22 AM   frmpg/s   bufpg/s    campg/s

09:57:23 AM    -81.19      0.00       0.00

09:57:24 AM      8.00      0.00       0.00

09:57:25 AM      0.00      2.02      -2.02

09:57:26 AM     15.84      0.00       0.00

09:57:27 AM    -19.80      0.00      64.36

Average:       -15.54      0.40      12.55

</pre>

[Listing 3.16](ch03lev1sec2.html#ch03ex16) shows that the system wrote ~53 pages of memory to disk during the third sample. The system has a relatively high fault count, which means that memory pages are being allocated and used. Fortunately, none of these are major faults, meaning that the system does not have to go to disk to fulfill the fault.

<a name="ch03ex16"></a>

##### Listing 3.16\.

<pre>

[ezolt@scrffy dvi]$ sar -B 1 5

Linux 2.6.8-1.521smp (scrffy)   10/25/2004

09:58:34 AM  pgpgin/s pgpgout/s   fault/s   majflt/s

09:58:35 AM      0.00      0.00   1328.28       0.00

09:58:36 AM      0.00      0.00    782.18       0.00

09:58:37 AM      0.00     53.06    678.57       0.00

09:58:38 AM      0.00      0.00    709.80       0.00

09:58:39 AM      0.00      0.00    717.17       0.00

Average:         0.00     10.42    842.48       0.00

</pre>

As you can see, <tt>sar</tt> is a powerful tool that enhances the functionality of the other system memory performance tools by adding the ability to archive, time stamp, and simultaneously collect many different types of <a name="iddle0728"></a><a name="iddle0729"></a><a name="iddle0730"></a>statistics.

<a name="ch03lev2sec10"></a>

#### 3.2.8\. /proc/meminfo

The Linux kernel <a name="iddle0731"></a><a name="iddle0732"></a><a name="iddle0733"></a>provides a user-readable text file called <tt>/proc/meminfo</tt> that displays current system-wide memory performance statistics. It provides a superset of the system-wide memory statistics that can be acquired with <tt>vmstat</tt>, <tt>top</tt>, <tt>free</tt>, and <tt>procinfo</tt>; but it is a little more difficult to use. If you want periodic updates, you must write a script or some code for such. If you want to store the memory performance information or coordinate it with CPU statistics, you must create a new tool or write a script. However, <tt>/proc/meminfo</tt> provides the most complete view of system memory usage.

<a name="ch03lev3sec20"></a>

##### 3.2.8.1 Memory Performance-Related Options

The information in <tt>/proc/meminfo</tt> can be retrieved with the <a name="iddle0734"></a><a name="iddle0735"></a><a name="iddle0736"></a>following command line:

<pre>cat /proc/meminfo

</pre>

This command displays the array of statistics described in [Table 3-11](ch03lev1sec2.html#ch03table11).

<a name="ch03table11"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 3-11\. <span class="docEmphasis"><tt>/proc/meminfo</tt></span> Memory Statistics (All in KB)

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0737"></a><a name="iddle0738"></a><a name="iddle0739"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>MemTotal</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0740"></a>The total amount of system physical memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>MemFree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0741"></a>The total amount of free physical memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Buffers</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0742"></a>The amount of memory used for pending disk writes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Cached</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0743"></a>The amount of memory used to cache disk reads.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SwapCached</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0744"></a>The amount of memory that exists in both the swap and the physical memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Active</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0745"></a>The amount of memory currently active in the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Inactive</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0746"></a>The amount of memory currently inactive and a candidate for swap.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0747"></a><a name="iddle0748"></a><a name="iddle0749"></a><tt>HighTotal</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0750"></a>The amount of high memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>HighFree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0751"></a>The amount of free high memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>LowTotal</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0752"></a>The amount of low memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>LowFree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0753"></a>The amount of free low memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SwapTotal</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0754"></a>The amount of swap memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SwapFree</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0755"></a>The amount of free swap memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Dirty</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0756"></a>Memory waiting to be written to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Writeback</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0757"></a>Memory currently being written to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

Mapped

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0758"></a>The total amount of memory brought into a process's virtual address space using <tt>mmap</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Slab</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0759"></a>The total amount of kernel slab memory (in KB).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Committed_AS</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0760"></a>The amount of memory required to almost never run out of memory with the current workload. Normally, the kernel hands out more memory than it actually has with the hope that applications overallocate. If all the applications were to use what they allocate, this is the amount of physical memory you would need.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>PageTables</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0761"></a>The amount of memory reserved for kernel page tables.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmallocTotal</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0762"></a>The amount of kernel memory usable for <tt>vmalloc</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmallocUsed</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0763"></a>The amount of kernel memory used for <tt>vmalloc</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmallocChunk</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0764"></a>The largest contiguous chunk of <tt>vmalloc</tt>'able memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>HugePages_Total</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0765"></a>The total size of all HugePages.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>HugePages_Free</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0766"></a>The total amount of free HugePages.

</td>

</tr>

</tbody>

</table>

<tt>/proc/meminfo</tt> provides a wealth of <a name="iddle0767"></a><a name="iddle0768"></a><a name="iddle0769"></a>information about the current state of the Linux memory subsystem.

<a name="ch03lev3sec21"></a>

##### 3.8.2.2 Example Usage

[Listing 3.17](ch03lev1sec2.html#ch03ex17) shows an <a name="iddle0770"></a><a name="iddle0771"></a><a name="iddle0772"></a>example output of <tt>/proc/meminfo</tt>. It shows some memory statistics that are similar to those we have seen with other tools. However, some statistics show new information. One, <tt>Dirty</tt>, shows that the system currently has 24KB of data waiting to be written to disk. Another, <tt>Commited_AS</tt>, shows that we need a little more memory (needed: 1068MB versus total: 1024MB) to avoid a potential out-of-memory situation.

<a name="ch03ex17"></a>

##### Listing 3.17\.

<pre>

[ezolt@scrffy /tmp]$ cat /proc/meminfo

MemTotal:      1034320 kB

MemFree:         10788 kB

Buffers:         29692 kB

Cached:         359496 kB

SwapCached:     113912 kB

Active:         704928 kB

Inactive:       222764 kB

HighTotal:           0 kB

HighFree:            0 kB

LowTotal:      1034320 kB

LowFree:         10788 kB

SwapTotal:     2040244 kB

SwapFree:      1756832 kB

Dirty:              24 kB

Writeback:           0 kB

Mapped:         604248 kB

Slab:            51352 kB

Committed_AS:  1093856 kB

PageTables:       9560 kB

VmallocTotal:  3088376 kB

VmallocUsed:     26600 kB

VmallocChunk:  3058872 kB

HugePages_Total:     0

HugePages_Free:      0

Hugepagesize:     2048 kB

</pre>

<tt>/proc/meminfo</tt> is the most complete place to gather system-wide Linux memory statistics. Because you can treat it as a text file, any custom script or <a name="iddle0773"></a><a name="iddle0774"></a><a name="iddle0775"></a>program can easily extract the statistics.