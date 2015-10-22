### 2.2\. Linux Performance Tools: CPU

Here begins our discussion of performance tools that enable you to extract information previously described.

<a name="ch02lev2sec5"></a>

#### 2.2.1\. vmstat (Virtual Memory Statistics)

<tt>vmstat</tt> stands <a name="iddle0074"></a><a name="iddle0075"></a><a name="iddle0076"></a>for virtual memory statistics, which indicates that it will give you information about the virtual memory system performance of your system. Fortunately, it actually does much more than that. <tt>vmstat</tt> is a great command to get a rough idea of how your system performs as a whole. It <a name="iddle0077"></a>tells you

*   How many processes are running

*   How the CPU is being used

*   How many interrupts the CPU receives

*   How many context switches the scheduler performs

It is an excellent tool to use to get a rough idea <a name="iddle0078"></a><a name="iddle0079"></a>of how the system performs.

<a name="ch02lev3sec1"></a>

##### 2.2.1.1 CPU Performance-Related Options

<tt>vmstat</tt> can be invoked with the following command line:

<pre>vmstat [-n] [-s] [delay [count]]

</pre>

<tt>vmstat</tt> can be run in two <a name="iddle0080"></a><a name="iddle0081"></a><a name="iddle0082"></a><a name="iddle0083"></a><a name="iddle0084"></a><a name="iddle0085"></a>modes: sample mode and average mode. If no parameters are specified, <tt>vmstat</tt> stat runs in average mode, where <tt>vmstat</tt> displays the average value for all the statistics since system boot. However, if a delay is specified, the first sample will be the average since system boot, but after that <tt>vmstat</tt> samples the system every delay seconds and prints out the statistics. [Table 2-1](ch02lev1sec2.html#ch02table01) describes the options that <tt>vmstat</tt> accepts.

<a name="ch02table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-1\. <span class="docEmphasis"><tt>vmstat</tt></span> Command-Line Options

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

<tt>-n</tt>

</td>

<td class="docTableCell" align="left" valign="top">

By default, <tt>vmstat</tt> periodically prints out the column headers for each performance statistic. This option disables that feature so that after the initial header, only performance data displays. This proves helpful if you want to import the output of <tt>vmstat</tt> into a spreadsheet.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0089"></a><a name="iddle0090"></a><a name="iddle0091"></a><tt>-s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays a one-shot details output of system statistics that <tt>vmstat</tt> gathers. The statistics are the totals since the system booted.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of time between <tt>vmstat</tt> samples.

</td>

</tr>

</tbody>

</table>

<tt>vmstat</tt> provides a variety of different output statistics that enable you to track different aspects of the system performance. [Table 2-2](ch02lev1sec2.html#ch02table02) describes those related to CPU performance. The next chapter covers those related to memory <a name="iddle0092"></a>performance.

<a name="ch02table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-2\. CPU-Specific <span class="docEmphasis"><tt>vmstat</tt></span> Output

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0093"></a><a name="iddle0094"></a>Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>r</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of currently runnable processes. These processes are not waiting on I/O and are ready to run. Ideally, the number of runnable processes would match the number of CPUs available.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>b</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of processes blocked and waiting for I/O to complete.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>forks</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The is the number of times a new process has been created.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>in</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of interrupts occurring on the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>cs</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of context switches happening on the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>us</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The is the total CPU time as a percentage spent on user processes (including "nice" time).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>sy</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The is the total CPU time as a percentage spent in system code. This includes time spent in the <tt>system</tt>, <tt>irq</tt>, and <tt>softirq</tt> state.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wa</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The is the total CPU time as a percentage spent waiting for I/O.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>id</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The is the total CPU time as a percentage that the system is idle.

</td>

</tr>

</tbody>

</table>

<tt>vmstat</tt> provides a good low-overhead view of system performance. Because all the performance statistics are in text form and are printed to standard output, it is easy to capture the data generated during a test and process or graph it later. Because <tt>vmstat</tt> is such a low-overhead tool, it is practical to keep it running on a console or in a window even on a very heavily loaded server when you need to monitor the health of the system at a <a name="iddle0095"></a>glance.

<a name="ch02lev3sec2"></a>

##### 2.2.1.2 Example Usage

As shown in [Listing 2.2](ch02lev1sec2.html#ch02ex02), if <tt>vmstat</tt> is run with no command-line parameters, it displays the average values for the statistics that it records since the system booted. This example shows that the system was nearly idle since boot, as indicated by the CPU usage columns, <a name="iddle0096"></a><a name="iddle0097"></a><a name="iddle0098"></a><a name="iddle0099"></a>under <tt>us</tt>, <tt>sys</tt>, <tt>wa</tt>, and <tt>id</tt>. The CPU spent 5 percent of the time since boot on user application code, 1 percent on system code, and the <a name="iddle0100"></a>rest, 94 percent sitting <a name="iddle0101"></a><a name="iddle0102"></a><a name="iddle0103"></a><a name="iddle0104"></a><a name="iddle0105"></a>idle.<a name="iddle0106"></a><a name="iddle0107"></a><a name="iddle0108"></a><a name="iddle0109"></a><a name="iddle0110"></a>

<a name="ch02ex02"></a>

##### Listing 2.2\.

<pre>[ezolt@scrffy tmp]$ vmstat

procs -----------memory---------- ---swap-- -----io---- --system--

<span class="docEmphStrong">----cpu----</span>

r  b   swpd   free   buff  cache   si   so    bi    bo   in    <span class="docEmphStrong">cs us sy id

wa</span>

1  0 181024  26284  35292 503048    0    0     3     2    6      <span class="docEmphStrong">1  5  1 94  0</span>

</pre>

Although <tt>vmstat</tt>'s <a name="iddle0111"></a><a name="iddle0112"></a><a name="iddle0113"></a>statistics since system boot can be useful to determine how heavily loaded the machine has been, <tt>vmstat</tt> is most useful when it runs in sampling mode, as shown in [Listing 2.3](ch02lev1sec2.html#ch02ex03). In sampling mode, <tt>vmstat</tt> prints the systems statistics after the number of seconds passed with the <tt>delay</tt> parameter. It does this sampling count a number of times. The first line of statistics in [Listing 2.3](ch02lev1sec2.html#ch02ex03) contains the system averages since boot, as before, but then the periodic sample continues after that. This example shows that there is very little activity on the system. We can see that no processes were blocked during the run by looking at the 0 in the <a name="iddle0114"></a><tt>b</tt>. We can also see, by looking in the <tt>r</tt> column, that fewer than 1 processes were running when <tt>vmstat</tt> sampled its <a name="iddle0115"></a><a name="iddle0116"></a><a name="iddle0117"></a><a name="iddle0118"></a><a name="iddle0119"></a><a name="iddle0120"></a>data.

<a name="ch02ex03"></a>

##### Listing 2.3\.

<pre>[ezolt@scrffy tmp]$ vmstat 2 5

<span class="docEmphStrong">procs</span>  -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

<span class="docEmphStrong">r  b</span>    swpd   free   buff  cache   si   so    bi    bo   in    cs us sy id wa

<span class="docEmphStrong">1  0</span>  181024  26276  35316 502960    0    0     3     2    6     1  5  1 94  0

<span class="docEmphStrong">1  0</span>  181024  26084  35316 502960    0    0     0     0 1318   772  1  0 98  0

<span class="docEmphStrong">0  0</span>  181024  26148  35316 502960    0    0     0    24 1314   734  1  0 98  0

<span class="docEmphStrong">0  0</span>  181024  26020  35316 502960    0    0     0     0 1315   764  2  0 98  0

<span class="docEmphStrong">0  0</span>  181024  25956  35316 502960    0    0     0     0 1310   764  2  0 98  0

</pre>

<tt>vmstat</tt> is an excellent way to record how a system behaves under a load or during a test condition. You can use <tt>vmstat</tt> to display how the system is behaving and, at the same time, save the result to a file by using the Linux <tt>tee</tt> command. ([Chapter 8](ch08.html#ch08), "[Utility Tools: Performance Tool Helpers](ch08.html#ch08)," describes the <tt>tee</tt> command in more detail.) If you only pass in the <tt>delay</tt> parameter, <tt>vmstat</tt> will sample indefinitely. Just start it before the test, and interrupt it after the test has completed. The output file can be imported into a spreadsheet, and used to see how the system reacts to the load or various system events. [Listing 2.4](ch02lev1sec2.html#ch02ex04) shows the output of this technique. In this example, we can look at the interrupt and context switches that the system is generating. We can see the total number of interrupts and context switches in the <a name="iddle0121"></a><a name="iddle0122"></a><tt>in</tt> and <tt>cs</tt> columns respectively.

The number of context switches looks good compared to the number of interrupts. The scheduler is switching processes less than the number of timer interrupts that are firing. This is most likely because the system is nearly idle, and most of the time when the timer interrupt fires, the scheduler does not have any work to do, so it does not switch from the idle process.

(Note: There is a bug in the version of <tt>vmstat</tt> that generated the following output. It causes the system average line of output to display incorrect values. This bug has been reported to the maintainer of <tt>vmstat</tt> and will be fixed <a name="iddle0123"></a><a name="iddle0124"></a><a name="iddle0125"></a>soon, hopefully.)

<a name="ch02ex04"></a>

##### Listing 2.4\.

<pre>[ezolt@scrffy ~/edid]$ vmstat 1 | tee /tmp/output

procs -----------memory---------- ---swap-- -----io----  <span class="docEmphStrong">--system--</span> ----cpu----

r  b   swpd   free   buff  cache   si   so    bi    bo    <span class="docEmphStrong">in    cs</span>  us sy id wa

0  1 201060  35832  26532 324112    0    0     3     2     <span class="docEmphStrong">6     2</span>  5  1  94  0

0  0 201060  35888  26532 324112    0    0    16     0  <span class="docEmphStrong">1138   358</span>  0  0  99  0

0  0 201060  35888  26540 324104    0    0     0    88  <span class="docEmphStrong">1163   371</span>  0  0 100  0

0  0 201060  35888  26540 324104    0    0     0     0  <span class="docEmphStrong">1133   345</span>  0  0 100  0

0  0 201060  35888  26540 324104    0    0     0    60  <span class="docEmphStrong">1174   351</span>  0  0 100  0

0  0 201060  35920  26540 324104    0    0     0     0  <span class="docEmphStrong">1150   408</span>  0  0 100  0

[Ctrl-C]

</pre>

More recent versions of <tt>vmstat</tt> can even extract more detailed information about a grab bag of different system statistics, as shown in [Listing 2.5](ch02lev1sec2.html#ch02ex05).

The next chapter discusses the memory statistics, but we look at the CPU statistics now. The first group of statistics, or "CPU ticks," shows how the CPU has spent its time since system boot, where a "tick" is a unit of time. Although the condensed <tt>vmstat</tt> output only showed four CPU states—<tt>us</tt>, <tt>sy</tt>, <tt>id</tt>, and <a name="iddle0126"></a><a name="iddle0127"></a><a name="iddle0128"></a><a name="iddle0129"></a><tt>wa</tt>—this shows how all the CPU ticks are distributed. In addition, we can see the total number of interrupts and context switches. One new addition is that <a name="iddle0130"></a>of <tt>forks</tt>, which is basically the number of new processes that have been created since <a name="iddle0131"></a><a name="iddle0132"></a><a name="iddle0133"></a>system boot.

<a name="ch02ex05"></a>

##### Listing 2.5\.

<pre>[ezolt@scrffy ~/edid]$ vmstat -s

      1034320  total memory

       998712  used memory

       698076  active memory

       176260  inactive memory

        35608  free memory

        26592  buffer memory

       324312  swap cache

      2040244  total swap

       201060  used swap

      1839184  free swap

      <span class="docEmphStrong">5279633 non-nice user cpu ticks

     28207739 nice user cpu ticks

      2355391 system cpu ticks

    628297350 idle cpu ticks

       862755 IO-wait cpu ticks

           34 IRQ cpu ticks

      1707439 softirq cpu ticks</span>

     21194571 pages paged in

     12677400 pages paged out

        93406 pages swapped in

       181587 pages swapped out

 <span class="docEmphStrong">1931462143 interrupts

    785963213 CPU context switches</span>

   1096643656 boot time

       <span class="docEmphStrong">578451 forks</span>

</pre>

<tt>vmstat</tt> provides a broad range of information about the performance of a Linux system. It is one of the core tools to use when investigating a problem with <a name="iddle0134"></a><a name="iddle0135"></a><a name="iddle0136"></a>a system.

<a name="ch02lev2sec6"></a>

#### 2.2.2\. top (v. 2.0.x)

<tt>top</tt> is the <a name="iddle0137"></a><a name="iddle0138"></a><a name="iddle0139"></a>Swiss army knife of Linux system-monitoring tools. It does a good job of putting a very large amount of system-wide performance information in a single screen. What you display can also be changed interactively; so if a particular problem creeps up as your system runs, you can modify what <tt>top</tt> is showing you.

By default, <tt>top</tt> presents a list, in decreasing order, of the top CPU-consuming processes. This enables you to quickly pinpoint which program is hogging the CPU. Periodically, <tt>top</tt> updates the list based on a delay that you can <a name="iddle0140"></a><a name="iddle0141"></a><a name="iddle0142"></a>specify. (It is initially 3 seconds.)

<a name="ch02lev3sec3"></a>

##### 2.2.2.1 CPU Performance-Related Options

<tt>top</tt> is invoked with the following command line:

<pre>top [d delay] [C] [H] [i] [n iter] [b]

</pre>

<tt>top</tt> actually takes options <a name="iddle0143"></a><a name="iddle0144"></a><a name="iddle0145"></a><a name="iddle0146"></a>in two modes: command-line options <a name="iddle0147"></a><a name="iddle0148"></a><a name="iddle0149"></a>and runtime options. The command-line options determine how <tt>top</tt> displays its information. [Table 2-3](ch02lev1sec2.html#ch02table03) shows the command-line options that influence the type and frequency of the performance statistics that <tt>top</tt> displays.

<a name="ch02table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-3\. <span class="docEmphasis"><tt>top</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0150"></a><a name="iddle0151"></a><a name="iddle0152"></a><a name="iddle0153"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>d delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Delay between statistic updates.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>n iterations</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Number of iterations before exiting. <tt>top</tt> updates the statistics <tt>iterations</tt> times.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>i</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Don't display processes that aren't using any of the CPU.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>H</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Show all the individual threads of an application rather than just display a total for each application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>C</tt>

</td>

<td class="docTableCell" align="left" valign="top">

In a hyperthreaded or SMP system, display the summed CPU statistics rather than the statistics for each CPU.

</td>

</tr>

</tbody>

</table>

As you run <tt>top</tt>, you might want to fine-tune what you are observing to investigate a particular problem. The output of <tt>top</tt> is highly customizable. [Table 2-4](ch02lev1sec2.html#ch02table04) describes options that change statistics shown during <a name="iddle0154"></a><a name="iddle0155"></a><a name="iddle0156"></a><a name="iddle0157"></a><tt>top</tt>'s runtime.

<a name="ch02table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-4\.

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

<tt>f</tt> or <tt>F</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays a configuration screen that enables you to select which process statistics display on the screen.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>o</tt> or <tt>O</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays a configuration screen that enables you to change the order of the displayed statistics.

</td>

</tr>

</tbody>

</table>

The options described in [Table 2-5](ch02lev1sec2.html#ch02table05) turn on or off the display of various system-wide information. It can be helpful to turn off unneeded statistics to fit more processes on the <a name="iddle0158"></a><a name="iddle0159"></a><a name="iddle0160"></a><a name="iddle0161"></a>screen.

<a name="ch02table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-5\. <span class="docEmphasis"><tt>top</tt></span> Runtime Output Toggles

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

<tt>l</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether the load average and uptime information will be updated and displayed.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>t</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles the display of how each CPU spends its time. It also toggles information about how many processes are currently running. Shows all the individual threads of an application instead of just displaying a total for each application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>m</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether information about the system memory usage will be shown on the screen. By default, the highest CPU consumers are displayed first. However, it might be more useful to sort by other characteristics.

</td>

</tr>

</tbody>

</table>

[Table 2-6](ch02lev1sec2.html#ch02table06) describes the different <a name="iddle0162"></a><a name="iddle0163"></a><a name="iddle0164"></a>sorting modes that <tt>top</tt> supports. Sorting by memory consumption is particular useful to figure out which process consumes the most amount of memory.

<a name="ch02table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-6\. <span class="docEmphasis"><tt>top</tt></span> Output Sorting/Display Options

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

<tt>P</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Sorts the tasks by their CPU usage. The highest CPU user displays first.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle0165"></a><tt>T</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Sorts the tasks by the amount of CPU time they have used so far. The highest amount displays first.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>N</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Sorts the tasks by their PID. The lowest PID displays first.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>A</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Sorts the tasks by their age. The newest PID is shown first. This is usually the opposite of "sort by PID."

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>i</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Hides tasks that are idle and are not consuming CPU.

</td>

</tr>

</tbody>

</table>

<tt>top</tt> provides system-wide information in addition to information about specific processes. [Table 2-7](ch02lev1sec2.html#ch02table07) covers <a name="iddle0166"></a><a name="iddle0167"></a><a name="iddle0168"></a>these statistics.

<a name="ch02table07"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-7\. <span class="docEmphasis"><tt>top</tt></span> Performance Statistics

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

<tt>us</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in user applications.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>sy</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the kernel.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ni</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in "nice"ed processes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>id</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent idle.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wa</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent waiting for I/O.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>hi</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the <tt>irq</tt> handlers.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>si</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the <tt>softirq</tt> handlers.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>load average</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The 1-minute, 5-minute, and 15-minute load average.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>%CPU</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The percentage of CPU that a particular process is consuming.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>PRI</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The priority value of the process, where a higher value indicates a higher priority. <tt>RT</tt> indicates that the task has real-time priority, a priority higher than the standard range.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>NI</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The nice value of the process. The higher the nice value, the less the system has to execute the process. Processes with high nice values tend to have very low priorities.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>WCHAN</tt>

</td>

<td class="docTableCell" align="left" valign="top">

If a process is waiting on an I/O, this shows which kernel function it is waiting in.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>STAT</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the current status of a process, where the process is either sleeping (<tt>S</tt>), running (<tt>R</tt>), zombied (killed but not yet dead) (<tt>Z</tt>), in an uninterruptable sleep (<tt>D</tt>), or being traced (<tt>T</tt>).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>TIME</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total amount CPU time (user and system) that this process has used since it started executing.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>COMMAND</tt>

</td>

<td class="docTableCell" align="left" valign="top">

That command that this process is executing.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>LC</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of the last CPU that this process was executing on.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>FLAGS</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether the load average and uptime information will be updated and displayed.

</td>

</tr>

</tbody>

</table>

<tt>top</tt> provides a large amount of information about the different running processes and is a great way to figure out which process is a resource <a name="iddle0169"></a><a name="iddle0170"></a><a name="iddle0171"></a>hog.

<a name="ch02lev3sec4"></a>

##### 2.2.2.2 Example Usage

[Listing 2.6](ch02lev1sec2.html#ch02ex06) is an example <a name="iddle0172"></a><a name="iddle0173"></a><a name="iddle0174"></a>run of <tt>top</tt>. Once it starts, it periodically updates the screen until you exit it. This demonstrates some of the system-wide statistics that <tt>top</tt> can generate. First, we see the load average of the system over the past 1, 5, and 15 minutes. As we can see, the system has started to get busy recently (because <tt>doom-3.x86</tt>). One CPU is busy with user code 90 percent of the time. The other is only spending ~13 percent of its time in user code. Finally, we can see that 73 of the processes are sleeping, and only 3 of them are currently <a name="iddle0175"></a><a name="iddle0176"></a><a name="iddle0177"></a>running.

<a name="ch02ex06"></a>

##### Listing 2.6\.

<pre>catan> top

 08:09:16  up 2 days, 18:44,  4 users,  <span class="docEmphStrong">load average: 0.95, 0.44, 0.17

76 processes: 73 sleeping, 3 running, 0 zombie, 0 stopped

CPU states:  cpu    user    nice  system    irq  softirq  iowait    idle

           total   51.5%    0.0%    3.9%   0.0%     0.0%    0.0%   44.6%

           cpu00   90.0%    0.0%    1.2%   0.0%     0.0%    0.0%    8.8%

           cpu01   13.0%    0.0%    6.6%   0.0%     0.0%    0.0%   80.4%</span>

Mem:  2037140k av, 1132120k used,  905020k free,       0k shrd,   86220k buff

       689784k active,             151528k inactive

Swap: 2040244k av,       0k used, 2040244k free                 322648k cached

  PID USER     PRI  NI  SIZE  RSS SHARE STAT %CPU %MEM   TIME CPU COMMAND

 <span class="docEmphStrong">7642 root      25   0  647M 379M  7664 R    49.9 19.0   2:58   0 doom.x86</span>

 7661 ezolt     15   0  1372 1372  1052 R     0.1  0.0   0:00   1 top

    1 root      15   0   528  528   452 S     0.0  0.0   0:05   1 init

    2 root      RT   0     0    0     0 SW    0.0  0.0   0:00   0 migration/0

    3 root      RT   0     0    0     0 SW    0.0  0.0   0:00   1 migration/1

    4 root      15   0     0    0     0 SW    0.0  0.0   0:00   0 keventd

    5 root      34  19     0    0     0 SWN   0.0  0.0   0:00   0 ksoftirqd/0

    6 root      34  19     0    0     0 SWN   0.0  0.0   0:00   1 ksoftirqd/1

    9 root      25   0     0    0     0 SW    0.0  0.0   0:00   0 bdflush

    7 root      15   0     0    0     0 SW    0.0  0.0   0:00   0 kswapd

    8 root      15   0     0    0     0 SW    0.0  0.0   0:00   1 kscand

   10 root      15   0     0    0     0 SW    0.0  0.0   0:00   1 kupdated

   11 root      25   0     0    0     0 SW    0.0  0.0   0:00   0 mdrecoveryd

</pre>

Now pressing F while <a name="iddle0178"></a><a name="iddle0179"></a><a name="iddle0180"></a><tt>top</tt> is running brings the configuration screen shown in [Listing 2.7](ch02lev1sec2.html#ch02ex07). When you press the keys indicated (A for PID, B for PPID, etc.), <tt>top</tt> toggles whether these statistics display in the previous screen. When all the desired statistics are selected, press Enter to return to <tt>top's</tt> initial screen, which now shows the current values of selected statistics. When configuring the statistics, all currently activated fields are capitalized in the Current Field Order line and have an asterisk (*) next to their name.<a name="iddle0181"></a><a name="iddle0182"></a><a name="iddle0183"></a>

<a name="ch02ex07"></a>

##### Listing 2.7\.

<pre>[ezolt@wintermute doc]$ top

(press 'F' while running)

   Current Field Order: AbcDgHIjklMnoTP|qrsuzyV{EFW[X

Toggle fields with a-z, any other key to return:

* A: PID        = Process Id

  B: PPID       = Parent Process Id

  C: UID        = User Id

* D: USER       = User Name

* E: %CPU       = CPU Usage

* F: %MEM       = Memory Usage

  G: TTY        = Controlling tty

* H: PRI        = Priority

* I: NI         = Nice Value

  J: PAGEIN     = Page Fault Count

  K: TSIZE      = Code Size (kb)

  L: DSIZE      = Data+Stack Size (kb)

* M: SIZE       = Virtual Image Size (kb)

  N: TRS        = Resident Text Size (kb)

  O: SWAP       = Swapped kb

* P: SHARE      = Shared Pages (kb)

  Q: A          = Accessed Page count

  R: WP         = Write Protected Pages

  S: D          = Dirty Pages

* T: RSS        = Resident Set Size (kb)

  U: WCHAN      = Sleeping in Function

* V: STAT       = Process Status

* W: TIME       = CPU Time

* X: COMMAND    = Command

  Y: LC         = Last used CPU (expect this to change regularly)

  Z: FLAGS      = Task Flags (see linux/sched.h)

</pre>

To show you how customizable <tt>top</tt> is, [Listing 2.8](ch02lev1sec2.html#ch02ex08) shows a highly configured output screen, which shows <a name="iddle0184"></a><a name="iddle0185"></a><a name="iddle0186"></a>only the <tt>top</tt> options relevant to CPU usage.

<a name="ch02ex08"></a>

##### Listing 2.8\.

<pre> 08:16:23  up 2 days, 18:52,  4 users,  load average: 1.07, 0.92, 0.49

76 processes: 73 sleeping, 3 running, 0 zombie, 0 stopped

CPU states:  cpu    user    nice  system    irq  softirq  iowait     idle

           total   48.2%    0.0%    1.5%   0.0%     0.0%    0.0%    50.1%

           cpu00    0.3%    0.0%    0.1%   0.0%     0.0%    0.0%    99.5%

           cpu01   96.2%    0.0%    2.9%   0.0%     0.0%    0.0%     0.7%

Mem:  2037140k av, 1133548k used,  903592k free,       0k shrd,    86232k buff

690812k active,             151536k inactive

Swap: 2040244k av,       0k used, 2040244k free                 322656k cached

  PID USER     PRI  NI WCHAN        FLAGS  LC STAT %CPU  TIME CPU COMMAND

 7642 root      25   0             100100   1 R    49.6 10:30   1 doom.x86

    1 root      15   0             400100   0 S     0.0  0:05   0 init

    2 root      RT   0                140   0 SW    0.0  0:00   0 migration/0

    3 root      RT   0                140   1 SW    0.0  0:00   1 migration/1

    4 root      15   0                 40   0 SW    0.0  0:00   0 keventd

    5 root      34  19                 40   0 SWN   0.0  0:00   0 ksoftirqd/0

    6 root      34  19                 40   1 SWN   0.0  0:00   1 ksoftirqd/1

    9 root      25   0                 40   0 SW    0.0  0:00   0 bdflush

    7 root      15   0                840   0 SW    0.0  0:00   0 kswapd

    8 root      15   0                 40   0 SW    0.0  0:00   0 kscand

   10 root      15   0                 40   0 SW    0.0  0:00   0 kupdated

   11 root      25   0                 40   0 SW    0.0  0:00   0 mdrecoveryd

   20 root      15   0             400040   0 SW    0.0  0:00   0 katad-1

</pre>

<tt>top</tt> provides an overview of system resource usage with a focus on <a name="iddle0187"></a><a name="iddle0188"></a><a name="iddle0189"></a>providing information about how various processes are consuming those resources. It is best used when interacting with the system directly because of the user-friendly and tool-unfriendly format of its output.

<a name="ch02lev2sec7"></a>

#### 2.2.3\. top (v. 3.x.x)

Recently, the <a name="iddle0190"></a><a name="iddle0191"></a><a name="iddle0192"></a>version of <tt>top</tt> provided by the most recent distributions has been completely overhauled, and as a result, many of the command-line and interaction options have changed. Although the basic ideas are similar, it has been streamlined, and a few different display modes have been added.

Again, <tt>top</tt> presents a list, in decreasing order, of the top CPU-consuming processes.

<a name="ch02lev3sec5"></a>

##### 2.2.3.1 CPU Performance-Related Options

<tt>top</tt> is invoked with the <a name="iddle0193"></a><a name="iddle0194"></a><a name="iddle0195"></a>following command line:

<pre>top [-d delay] [-n iter] [-i] [-b]

</pre>

<tt>top</tt> actually takes options in two <a name="iddle0196"></a><a name="iddle0197"></a><a name="iddle0198"></a><a name="iddle0199"></a><a name="iddle0200"></a><a name="iddle0201"></a><a name="iddle0202"></a>modes: command-line options and runtime options. The command-line options determine how <tt>top</tt> displays its information. [Table 2-8](ch02lev1sec2.html#ch02table08) shows the command-line options that influence the type and frequency of the performance statistics that <tt>top</tt> will display.

<a name="ch02table08"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-8\. <span class="docEmphasis"><tt>top</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0203"></a><a name="iddle0204"></a><a name="iddle0205"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Delay between statistic updates.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n iterations</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Number of iterations before exiting. <tt>top</tt> updates the statistics' <tt>iterations</tt> times.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-i</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This option changes whether or not idle processes display.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-b</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Run in batch mode. Typically, <tt>top</tt> shows only a single screenful of information, and processes that don't fit on the screen never display. This option shows all the processes and can be very useful if you are saving <tt>top</tt>'s output to a file or piping the output to another command for processing.

</td>

</tr>

</tbody>

</table>

As you run <tt>top</tt>, you <a name="iddle0206"></a><a name="iddle0207"></a><a name="iddle0208"></a><a name="iddle0209"></a>may want to fine-tune what you are observing to investigate a particular problem. Like the 2.x version of <tt>top</tt>, the output of <tt>top</tt> is highly customizable. [Table 2-9](ch02lev1sec2.html#ch02table09) describes options that change statistics shown during <tt>top</tt>'s runtime.

<a name="ch02table09"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-9\. <span class="docEmphasis"><tt>top</tt></span> Runtime Options

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0210"></a><a name="iddle0211"></a><a name="iddle0212"></a><a name="iddle0213"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>A</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays an "alternate" display of process information that shows top consumers of various system resources.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>I</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether <tt>top</tt> will divide the CPU usage by the number of CPUs on the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

For example, if a process was consuming all of both CPUs on a two-CPU system, this toggles whether <tt>top</tt> displays a CPU usage of 100% or 200%.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>f</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays a configuration screen that enables you to select which process statistics display on the screen.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>o</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays a configuration screen that enables you to change the order of the displayed statistics.

</td>

</tr>

</tbody>

</table>

The options described in [Table 2-10](ch02lev1sec2.html#ch02table10) turn on or off the display of various system-wide information. It can be helpful to turn off unneeded statistics to fit more processes on the screen.

<a name="ch02table10"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-10\. <span class="docEmphasis"><tt>top</tt></span> Runtime Output Toggles

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0214"></a><a name="iddle0215"></a><a name="iddle0216"></a><a name="iddle0217"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>1 (numeral 1)</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether the CPU usage will be broken down to the individual usage or shown as a total.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>l</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This toggles whether the load average and uptime information will be updated and displayed.

</td>

</tr>

</tbody>

</table>

<tt>top v3.x</tt> provides system-wide information in addition to information about specific processes similar to <a name="iddle0218"></a><a name="iddle0219"></a><a name="iddle0220"></a>those of <tt>top v2.x</tt>. These statistics are covered in [Table 2-11](ch02lev1sec2.html#ch02table11).

<a name="ch02table11"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-11\. <span class="docEmphasis"><tt>top</tt></span> Performance Statistics

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

<tt>us</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in user applications.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>sy</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the kernel.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ni</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in "nice"ed processes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>id</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent idle.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wa</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent waiting for I/O.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>hi</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the <tt>irq</tt> handlers.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>si</tt>

</td>

<td class="docTableCell" align="left" valign="top">

CPU time spent in the <tt>softirq</tt> handlers.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>load average</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The 1-minute, 5-minute, and 15-minute load average.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>%CPU</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The percentage of CPU that a particular process is consuming.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>PRI</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The priority value of the process, where a higher value indicates a higher priority. <tt>RT</tt> indicates that the task has real-time priority, a priority higher than the standard range.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>NI</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The nice value of the process. The higher the nice value, the less the system has to execute the process. Processes with high nice values tend to have very low priorities.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>WCHAN</tt>

</td>

<td class="docTableCell" align="left" valign="top">

If a process is waiting on an I/O, this shows which kernel function it is waiting in.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>TIME</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total amount CPU time (user and system) that this process has used since it started executing.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>COMMAND</tt>

</td>

<td class="docTableCell" align="left" valign="top">

That command that this process is executing.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>S</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the current status of a process, where the process is either sleeping (<tt>S</tt>), running (<tt>R</tt>), zombied (killed but not yet dead) (<tt>Z</tt>), in an uninterruptable sleep (<tt>D</tt>), or being traced (<tt>T</tt>).

</td>

</tr>

</tbody>

</table>

<tt>top</tt> provides a large amount of information about the different running processes and is a great way to figure out which process is a resource hog. The v.3 version of <tt>top</tt> has trimmed-down <tt>top</tt> and added some alternative views of similar data.

<a name="ch02lev3sec6"></a>

##### 2.2.3.2 Example Usage

[Listing 2.9](ch02lev1sec2.html#ch02ex09)<a name="iddle0221"></a><a name="iddle0222"></a><a name="iddle0223"></a> is an example run of <tt>top</tt> v3.0\. Again, it will periodically update the screen until you exit it. The statistics are similar to those of <tt>top</tt> v2.x, but are named slightly differently.

<a name="ch02ex09"></a>

##### Listing 2.9\.

<pre>catan> top

top - 08:52:21 up 19 days, 21:38, 17 users,   <span class="docEmphStrong">load average: 1.06, 1.13, 1.15

Tasks: 149 total,   1 running, 146 sleeping,    1 stopped,   1 zombie

Cpu(s):  0.8% us,  0.4% sy,  4.2% ni, 94.2% id,   0.1% wa,  0.0% hi,  0.3% si</span>

Mem:   1034320k total,  1023188k used,    11132k  free,    39920k buffers

Swap:  2040244k total,   214496k used,  1825748k  free,   335488k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM     TIME+  COMMAND

26364 root      16   0  400m  68m 321m S  3.8  6.8  379:32.04 X

26737 ezolt     15   0 71288  45m  21m S  1.9  4.5    6:32.04 gnome-terminal

29114 ezolt     15   0 34000  22m  18m S  1.9  2.2   27:57.62 gnome-system-mo

 9581 ezolt     15   0  2808 1028 1784 R  1.9  0.1    0:00.03 top

    1 root      16   0  2396  448 1316 S  0.0  0.0    0:01.68 init

    2 root      RT   0     0    0    0 S  0.0  0.0    0:00.68 migration/0

    3 root      34  19     0    0    0 S  0.0  0.0    0:00.01 ksoftirqd/0

    4 root      RT   0     0    0    0 S  0.0  0.0    0:00.27 migration/1

    5 root      34  19     0    0    0 S  0.0  0.0    0:00.01 ksoftirqd/1

    6 root      RT   0     0    0    0 S  0.0  0.0    0:22.49 migration/2

    7 root      34  19     0    0    0 S  0.0  0.0    0:00.01 ksoftirqd/2

    8 root      RT   0     0    0    0 S  0.0  0.0    0:37.53 migration/3

    9 root      34  19     0    0    0 S  0.0  0.0    0:00.01 ksoftirqd/3

   10 root       5 -10     0    0    0 S  0.0  0.0    0:01.74 events/0

   11 root       5 -10     0    0    0 S  0.0  0.0    0:02.77 events/1

   12 root       5 -10     0    0    0 S  0.0  0.0    0:01.79 events/2

</pre>

Now pressing f while <tt>top</tt> is running brings the configuration screen shown in [Listing 2.10](ch02lev1sec2.html#ch02ex10). When you press the keys indicated (A for PID, B for PPID, etc.), <tt>top</tt> toggles whether these statistics display in the previous screen. When all the desired statistics are selected, press Enter to return to <tt>top</tt>'s initial screen, which now shows the current values of selected statistics. When you are configuring the statistics, all currently activated fields are capitalized in the Current Field Order line and have and asterisk (*) next to their name. Notice that most of statistics are similar, but the names have slightly changed.

<a name="ch02ex10"></a>

##### Listing 2.10\.

<pre>(press 'f' while running)

Current Fields:  AEHIOQTWKNMbcdfgjplrsuvyzX  for window 1:Def

Toggle fields via field letter, type any other key to return

* A: PID        = Process Id                 u: nFLT       = Page Fault count

* E: USER       = User Name                  v: nDRT       = Dirty Pages count

* H: PR         = Priority                   y: WCHAN      = Sleeping in Function

* I: NI         = Nice value                 z: Flags      = Task Flags <sched.h>

* O: VIRT       = Virtual Image (kb)       * X: COMMAND    = Command name/line

* Q: RES        = Resident size (kb)

* T: SHR        = Shared Mem size (kb)     Flags field:

* W: S          = Process Status             0x00000001  PF_ALIGNWARN

* K: %CPU       = CPU usage                  0x00000002  PF_STARTING

* N: %MEM       = Memory usage (RES)         0x00000004  PF_EXITING

* M: TIME+      = CPU Time, hundredths       0x00000040  PF_FORKNOEXEC

  b: PPID       = Parent Process Pid         0x00000100  PF_SUPERPRIV

  c: RUSER      = Real user name             0x00000200  PF_DUMPCORE

  d: UID        = User Id                    0x00000400  PF_SIGNALED

  f: GROUP      = Group Name                 0x00000800  PF_MEMALLOC

  g: TTY        = Controlling Tty            0x00002000  PF_FREE_PAGES (2.5)

  j: #C         = Last used cpu (SMP)        0x00008000  debug flag (2.5)

  p: SWAP       = Swapped size (kb)          0x00024000  special threads (2.5)

  l: TIME       = CPU Time                   0x001D0000  special states (2.5)

  r: CODE       = Code size (kb)             0x00100000  PF_USEDFPU (thru 2.4)

  s: DATA       = Data+Stack size (kb)

</pre>

[Listing 2.11](ch02lev1sec2.html#ch02ex11) shows the new <a name="iddle0224"></a><a name="iddle0225"></a><a name="iddle0226"></a>output mode of <tt>top</tt>, where many different statistics are sorted and displayed on the same screen.

<a name="ch02ex11"></a>

##### Listing 2.11\.

<pre>(press 'F' while running)

1:Def - 09:00:48 up 19 days, 21:46, 17 users,  load average: 1.01, 1.06, 1.10

Tasks: 144 total,   1 running, 141 sleeping,   1 stopped,   1 zombie

Cpu(s):  1.2% us,  0.9% sy,  0.0% ni, 97.9% id,  0.0% wa,  0.0% hi,  0.0% si

Mem:   1034320k total,  1024020k used,    10300k free,    39408k buffers

Swap:  2040244k total,   214496k used,  1825748k free,   335764k cached

<span class="docEmphStrong">1  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND</span>

 29114 ezolt     16   0 34112  22m  18m S  3.6  2.2  28:15.06 gnome-system-mo

 26364 root      15   0  400m  68m 321m S  2.6  6.8  380:01.09 X

  9689 ezolt     16   0  3104 1092 1784 R  1.0  0.1    0:00.09 top

<span class="docEmphStrong">2  PID  PPID    TIME+  %CPU %MEM  PR  NI S  VIRT SWAP   RES  UID COMMAND</span>

 30403 24989   0:00.03  0.0  0.1  15   0 S  5808 4356  1452 9336 bash

 29510 29505   7:19.59  0.0  5.9  16   0 S  125m  65m   59m 9336 firefox-bin

 29505 29488   0:00.00  0.0  0.1  16   0 S  5652 4576  1076 9336 run-mozilla.sh

<span class="docEmphStrong">3  PID %MEM  VIRT SWAP  RES CODE DATA  SHR nFLT nDRT S  PR  NI %CPU COMMAND</span>

  8414 25.0  374m 121m 252m  496 373m  98m 1547    0 S  16   0  0.0 soffice.bin

 26364  6.8  400m 331m  68m 1696 398m 321m 2399    0 S  15   0  2.6 X

 29510  5.9  125m  65m  59m   64 125m  31m  253    0 S  16   0  0.0 firefox-bin

 26429  4.7 59760  10m  47m  404  57m  12m 1247    0 S  15   0  0.0 metacity

<span class="docEmphStrong">4  PID  PPID  UID USER     RUSER    TTY         TIME+  %CPU %MEM S COMMAND</span>

    1371   1   43 xfs      xfs      ?          0:00.10  0.0  0.1 S xfs

    1313   1   51 smmsp    smmsp    ?          0:00.08  0.0  0.2 S sendmail

     982   1   29 rpcuser  rpcuser  ?          0:00.07  0.0  0.1 S rpc.statd

     963   1   32 rpc      rpc      ?          0:06.23  0.0  0.1 S portmap

</pre>

<tt>top</tt> v3.x provides a slightly cleaner interface to <tt>top</tt>. It simplifies some aspects of it and provides a nice "summary" information screen that displays many of the resource consumers in the <a name="iddle0227"></a><a name="iddle0228"></a><a name="iddle0229"></a>system.

<a name="ch02lev2sec8"></a>

#### 2.2.4\. procinfo (Display Info from the /proc File System)

Much like <tt>vmstat</tt>, <tt>procinfo</tt> provides <a name="iddle0230"></a><a name="iddle0231"></a><a name="iddle0232"></a>a view of the system-wide performance characteristics. Although some of the information that it provides is similar to that of <tt>vmstat</tt>, it also provides information about the number of interrupts that the CPU received for each device. Its output format is a little more readable than <tt>vmstat</tt>, but it takes up much <a name="iddle0233"></a>more screen space.

<a name="ch02lev3sec7"></a>

##### 2.2.4.1 CPU Performance-Related Options

<tt>procinfo</tt> is invoked <a name="iddle0234"></a><a name="iddle0235"></a><a name="iddle0236"></a><a name="iddle0237"></a>with the following command:

<pre>procinfo [-f] [-d] [-D] [-n sec] [-f file]

</pre>

[Table 2-12](ch02lev1sec2.html#ch02table12) describes the different options that change the output and the frequency of the samples that <tt>procinfo</tt> displays.

<a name="ch02table12"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-12\. <span class="docEmphasis"><tt>procinfo</tt></span> Command-Line Options

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

<tt>-f</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Runs <tt>procinfo</tt> in full-screen mode

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Displays statistics change between samples rather than totals

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-D</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Displays statistic totals rather than rate of change

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n sec</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Number of seconds to pause between each sample

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-Ffile</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Sends the output of <tt>procinfo</tt> to a file

</td>

</tr>

</tbody>

</table>

[Table 2-13](ch02lev1sec2.html#ch02table13) shows the CPU statistics that <tt>procinfo</tt> <a name="iddle0238"></a><a name="iddle0239"></a><a name="iddle0240"></a><a name="iddle0241"></a>gathers.

<a name="ch02table13"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-13\. <span class="docEmphasis"><tt>procinfo</tt></span> CPU Statistics

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0242"></a><a name="iddle0243"></a><a name="iddle0244"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>user</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of user time that the CPU has spent in days, hours, and minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>nice</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of nice time that the CPU has spent in days, hours, and minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>system</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of system time that the CPU has spent in days, hours, and minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>idle</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the amount of idle time that the CPU has spent in days, hours, and minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>irq 0- N</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This displays the number of the <tt>irq</tt>, the amount that has fired, and which kernel driver is responsible for it.

</td>

</tr>

</tbody>

</table>

Much like <tt>vmstat</tt> or <tt>top</tt>, <tt>procinfo</tt> is a low-overhead command that is good to leave running in a console or window on the screen. It gives a good indication of a system's health and <a name="iddle0245"></a><a name="iddle0246"></a><a name="iddle0247"></a>performance.

<a name="ch02lev3sec8"></a>

##### 2.2.4.2 Example Usage

Calling <tt>procinfo</tt> without <a name="iddle0248"></a><a name="iddle0249"></a><a name="iddle0250"></a>any command options yields output similar to [Listing 2.12](ch02lev1sec2.html#ch02ex12). Without any options, <tt>procinfo</tt> displays only one screenful of status and then exits. <tt>procinfo</tt> is more useful when it is periodically updated using the <tt>-n second</tt> options. This enables you to see how the system's performance is changing in real time.

<a name="ch02ex12"></a>

##### Listing 2.12\.

<pre>[ezolt@scrffy ~/mail]$ procinfo

Linux 2.4.18-3bigmem (bhcompile@daffy) (gcc 2.96 20000731 ) #1 4CPU [scrffy]

Memory:      Total        Used        Free      Shared     Buffers       Cached

Mem:       1030784      987776       43008           0       35996       517504

Swap:      2040244       17480     2022764

Bootup: Thu Jun  3 09:20:22 2004     <span class="docEmphStrong">Load average: 0.47 0.32 0.26</span> 1/118 10378

<span class="docEmphStrong">user  :       3:18:53.99   2.7%</span>   page in :  1994292  disk 1:       20r       0w

<span class="docEmphStrong">nice  :       0:00:22.91   0.0%</span>   page out:  2437543  disk 2:   247231r  131696w

<span class="docEmphStrong">system:       3:45:41.20   3.1%</span>   swap in :      996

<span class="docEmphStrong">idle  :   4d 15:56:17.10  94.0%</span>   swap out:     4374

uptime:   1d  5:45:18.80          context : 64608366

<span class="docEmphStrong">irq  0:  10711880 timer                  irq 12:   1319185 PS/2 Mouse

irq  1:     94931 keyboard               irq 14:   7144432 ide0

irq  2:         0 cascade [4]            irq 16:        16 aic7xxx

irq  3:         1                        irq 18:   4152504 nvidia

irq  4:         1                        irq 19:         0 usb-uhci

irq  6:         2                        irq 20:   4772275 es1371

irq  7:         1                        irq 22:    384919 aic7xxx

irq  8:         1 rtc                    irq 23:   3797246 usb-uhci, eth0</span>

</pre>

As you can see <a name="iddle0251"></a><a name="iddle0252"></a><a name="iddle0253"></a>from [Listing 2.12](ch02lev1sec2.html#ch02ex12), <tt>procinfo</tt> provides a reasonable overview of the system. We can see that, once again for the user, nice, system, and idle time, the system is not very busy. One interesting thing to notice is that <tt>procinfo</tt> claims that the system has spent more idle time than the system has been running (as indicated by the uptime). This is because the system actually has four CPUs, so for every day of wall time, four days of CPU time passes. The load average confirms that the system has been relatively work-free for the recent past. For the past minute, on the average, the system had less than one process ready to run; a load average of .47 indicates that a single process was ready to run only 47 percent of the time. On a four-CPU system, this large amount of CPU power is going to waste.

<tt>procinfo</tt> also gives us a good view of what devices on the system are causing interrupts. We can see that the Nvidia card (<tt>nvidia</tt>), IDE controller (<tt>ide0</tt>), Ethernet device (<tt>eth0</tt>), and sound card (<tt>es1371</tt>) have a relatively high number of interrupts. This is as one would expect for a desktop workstation.

<tt>procinfo</tt> has the advantage of putting many of the system-wide performance statistics within a single screen, enabling you to see how the system is performing as a whole. It lacks details about network and disk performance, but it provide a good system-wide detail of the CPU and memory performance. One limitation that can be significant is the fact that <tt>procinfo</tt> does not report when the CPU is in the <tt>iowait</tt>, <tt>irq</tt>, or <tt>softirq</tt> <a name="iddle0254"></a><a name="iddle0255"></a><a name="iddle0256"></a>mode.

<a name="ch02lev2sec9"></a>

#### 2.2.5\. gnome-system-monitor

<tt>gnome-system-monitor</tt> is, in many ways, a graphical counterpart of <tt>top</tt>. It enables you to graphically monitor individual processes and observe the load on the system based on the graphs that it displays.

<a name="ch02lev3sec9"></a>

##### 2.2.5.1 CPU Performance-Related Options

<tt>gnome-system-monitor</tt> can be <a name="iddle0257"></a><a name="iddle0258"></a><a name="iddle0259"></a>invoked from the Gnome menu. (Under Red Hat 9 and greater, this is under System Tools > System Monitor.) However, it can also be invoked using the following command:

<pre>gnome-system-monitor

</pre>

<tt>gnome-system-monitor</tt> has no relevant command-line options that affect the CPU performance measurements. However, some of the statistics shown can be modified by selecting <tt>gnome-system-monitor's</tt> Edit > Preferences <a name="iddle0260"></a><a name="iddle0261"></a><a name="iddle0262"></a>menu entry.

<a name="ch02lev3sec10"></a>

##### 2.2.5.2 Example Usage

When you <a name="iddle0263"></a><a name="iddle0264"></a><a name="iddle0265"></a>launch <tt>gnome-system-monitor</tt>, it creates a window similar to [Figure 2-1](ch02lev1sec2.html#ch02fig01). This window shows information about the amount of CPU and memory that a particular process is using. It also shows information about the parent/child relationships between each process.

<a name="ch02fig01"></a>

<center>

##### Figure 2-1\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/02fig01.jpg)

</center>

[Figure 2-2](ch02lev1sec2.html#ch02fig02) shows a graphical view of system load and memory usage. This is really what distinguishes <tt>gnome-system-monitor</tt> from <tt>top</tt>. You can easily see the current state of the system and how it compares to the previous <a name="iddle0266"></a><a name="iddle0267"></a><a name="iddle0268"></a>state.

<a name="ch02fig02"></a>

<center>

##### Figure 2-2\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/02fig02.jpg)

</center>

The graphical view of data provided by <tt>gnome-system-monitor</tt> can make it easier and faster to determine the state of the system, and how its behavior changes over time. It also makes it easier to navigate the system-wide process <a name="iddle0269"></a><a name="iddle0270"></a><a name="iddle0271"></a>information.

<a name="ch02lev2sec10"></a>

#### 2.2.6\. mpstat (Multiprocessor Stat)

<tt>mpstat</tt> is a <a name="iddle0272"></a><a name="iddle0273"></a><a name="iddle0274"></a>fairly simple command that shows you how your processors are behaving based on time. The biggest benefit of <tt>mpstat</tt> is that it shows the time next to the statistics, so you can look for a correlation between CPU usage and time of day.

If you have multiple CPUs or hyperthreading-enabled <a name="iddle0275"></a>CPUs, <tt>mpstat</tt> can also break down CPU usage based on the processor, so you can see whether a particular processor is doing more work than the others. You can select which individual processor you want to monitor or you can ask <tt>mpstat</tt> to monitor all of them.

<a name="ch02lev3sec11"></a>

##### 2.2.6.1 CPU Performance-Related Options

<tt>mpstat</tt> can be <a name="iddle0276"></a><a name="iddle0277"></a><a name="iddle0278"></a>invoked using the following command line:

<pre>mpstat [ -P { cpu | ALL } ] [ delay [ count ] ]

</pre>

Once again, <tt>delay</tt> specifies how often the samples will be taken, and <tt>count</tt> determines how many times it will be run. [Table 2-14](ch02lev1sec2.html#ch02table14) describes the command-line options of <tt>mpstat</tt>.

<a name="ch02table14"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-14\. <span class="docEmphasis"><tt>mpstat</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0279"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-P { cpu | ALL</tt> }

</td>

<td class="docTableCell" align="left" valign="top">

This option tells <tt>mpstat</tt> which CPUs to monitor. <tt>cpu</tt> is the number between 0 and the total CPUs minus 1.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This specifies how long <tt>mpstat</tt> waits between samples.

</td>

</tr>

</tbody>

</table>

<tt>mpstat</tt> provides similar information to the other CPU performance tools, but it allows the information to be attributed to each of the processors in a particular system. [Table 2-15](ch02lev1sec2.html#ch02table15) describes the options that it <a name="iddle0280"></a><a name="iddle0281"></a><a name="iddle0282"></a>supports.

<a name="ch02table15"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-15\. <span class="docEmphasis"><tt>mpstat</tt></span> CPU Statistics

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0283"></a><a name="iddle0284"></a><a name="iddle0285"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>user</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of user time that the CPU has spent during the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>nice</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample running low-priority (or nice) processes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>system</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of system time that the CPU has spent during the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>iowait</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample waiting on I/O.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>irq</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample handling interrupts.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>softirq</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample handling work that needed to be done by the kernel after an interrupt has been handled.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>idle</tt><a name="iddle0286"></a>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent idle during the previous sample.

</td>

</tr>

</tbody>

</table>

<tt>mpstat</tt> is a good tool for providing a breakdown of how each <a name="iddle0287"></a><a name="iddle0288"></a><a name="iddle0289"></a>of the processors is performing. Because <tt>mpstat</tt> provides a per-CPU breakdown, you can identify whether one of the processors is becoming overloaded.

<a name="ch02lev3sec12"></a>

##### 2.2.6.2 Example Usage

First, we ask <tt>mpstat</tt> to <a name="iddle0290"></a><a name="iddle0291"></a><a name="iddle0292"></a>show us the CPU statistics for processor number 0\. This is shown in [Listing 2.13](ch02lev1sec2.html#ch02ex13).

<a name="ch02ex13"></a>

##### Listing 2.13\.

<pre>[ezolt@scrffy sysstat-5.1.1]$ ./mpstat -P 0 1 10

Linux 2.6.8-1.521smp (scrffy)   10/20/2004

07:12:02 PM  CPU   %user   %nice    %sys %iowait    %irq   %soft   %idle     intr/s

07:12:03 PM    0    9.80    0.00    1.96    0.98    0.00    0.00   87.25    1217.65

07:12:04 PM    0    1.01    0.00    0.00    0.00    0.00    0.00   98.99    1112.12

07:12:05 PM    0    0.99    0.00    0.00    0.00    0.00    0.00   99.01    1055.45

07:12:06 PM    0    0.00    0.00    0.00    0.00    0.00    0.00  100.00    1072.00

07:12:07 PM    0    0.00    0.00    0.00    0.00    0.00    0.00  100.00    1075.76

07:12:08 PM    0    1.00    0.00    0.00    0.00    0.00    0.00   99.00    1067.00

07:12:09 PM    0    4.90    0.00    3.92    0.00    0.00    0.98   90.20    1045.10

07:12:10 PM    0    0.00    0.00    0.00    0.00    0.00    0.00  100.00    1069.70

07:12:11 PM    0    0.99    0.00    0.99    0.00    0.00    0.00   98.02    1070.30

07:12:12 PM    0    3.00    0.00    4.00    0.00    0.00    0.00   93.00    1067.00

Average:       0    2.19    0.00    1.10    0.10    0.00    0.10   96.51    1085.34

</pre>

[Listing 2.14](ch02lev1sec2.html#ch02ex14) shows a similar command on very unloaded CPUs <a name="iddle0293"></a><a name="iddle0294"></a><a name="iddle0295"></a>that both have hyperthreading. You can see how the stats for all the CPUs are shown. One interesting observation in this output is the fact that one CPU seems to handle all the interrupts. If the system was heavy loaded with I/O, and all the interrupts were being handed by a single processor, this could be the cause of a bottleneck, because one CPU is overwhelmed, and the rest are waiting for work to do. You would be able to see this with mpstat, if the processor handling all the interrupts had no idle time, whereas the other processors did.

<a name="ch02ex14"></a>

##### Listing 2.14\.

<pre>[ezolt@scrffy sysstat-5.1.1]$ ./mpstat -P ALL 1 2

Linux 2.6.8-1.521smp (scrffy)   10/20/2004

07:13:21 PM  CPU   %user   %nice    %sys %iowait    %irq   %soft   %idle     intr/s

07:13:22 PM  all    3.98    0.00    1.00    0.25    0.00    0.00   94.78    1322.00

07:13:22 PM    0    2.00    0.00    0.00    1.00    0.00    0.00   97.00    1137.00

07:13:22 PM    1    6.00    0.00    2.00    0.00    0.00    0.00   93.00     185.00

07:13:22 PM    2    1.00    0.00    0.00    0.00    0.00    0.00   99.00       0.00

07:13:22 PM    3    8.00    0.00    1.00    0.00    0.00    0.00   91.00       0.00

07:13:22 PM  CPU   %user   %nice    %sys %iowait    %irq   %soft   %idle     intr/s

07:13:23 PM  all    2.00    0.00    0.50    0.00    0.00    0.00   97.50    1352.53

07:13:23 PM    0    0.00    0.00    0.00    0.00    0.00    0.00  100.00    1135.35

07:13:23 PM    1    6.06    0.00    2.02    0.00    0.00    0.00   92.93     193.94

07:13:23 PM    2    0.00    0.00    0.00    0.00    0.00    0.00  101.01      16.16

07:13:23 PM    3    1.01    0.00    1.01    0.00    0.00    0.00  100.00       7.07

Average:     CPU   %user   %nice    %sys %iowait    %irq   %soft   %idle     intr/s

Average:     all    2.99    0.00    0.75    0.12    0.00    0.00   96.13    1337.19

Average:       0    1.01    0.00    0.00    0.50    0.00    0.00   98.49    1136.18

Average:       1    6.03    0.00    2.01    0.00    0.00    0.00   92.96     189.45

Average:       2    0.50    0.00    0.00    0.00    0.00    0.00  100.00       8.04

Average:       3    4.52    0.00    1.01    0.00    0.00    0.00   95.48       3.52

</pre>

<tt>mpstat</tt> can be used to determine whether the CPUs are fully utilized and relatively balanced. By observing the number of interrupts each CPU is handling, it is possible to find an imbalance. Details on how to control where interrupts are routing are provided in the kernel source <a name="iddle0296"></a><a name="iddle0297"></a><a name="iddle0298"></a>under <tt>Documentation/IRQ-affinity.txt</tt>.

<a name="ch02lev2sec11"></a>

#### 2.2.7\. sar (System Activity Reporter)

<tt>sar</tt> has yet another <a name="iddle0299"></a><a name="iddle0300"></a><a name="iddle0301"></a>approach to collecting system data. <tt>sar</tt> can efficiently record system performance data collected into binary files that can be replayed at a later date. <tt>sar</tt> is a low-overhead way to record information about how the system is performing.

The <tt>sar</tt> command can be used to record performance information, replay previous recorded information, and display real-time information about the current system. The output of the <tt>sar</tt> command can be formatted to make it easy to pipe to relational databases or to other Linux commands <a name="iddle0302"></a>for processing.

<a name="ch02lev3sec13"></a>

##### 2.2.7.1 CPU Performance-Related Options

<tt>sar</tt> can be <a name="iddle0303"></a><a name="iddle0304"></a><a name="iddle0305"></a>invoked with the following command line:

<pre>sar [options] [ delay [ count ] ]

</pre>

Although <tt>sar</tt> reports about many different areas of Linux, the statistics are of two different forms. One set of statistics is the instantaneous value at the time of the sample. The other is a rate since the last sample. [Table 2-16](ch02lev1sec2.html#ch02table16) describes the command-line options of <tt>sar</tt>.

<a name="ch02table16"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-16\. <span class="docEmphasis"><tt>sar</tt></span> Command-Line Options

</caption><colgroup><col width="270"><col width="230"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0306"></a><a name="iddle0307"></a><a name="iddle0308"></a><a name="iddle0309"></a>Option

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

This reports information about how many processes are being created per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-I {irq | SUM | ALL | XALL</tt>}

</td>

<td class="docTableCell" align="left" valign="top">

This reports the rates that interrupts have been occurring in the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-P {cpu | ALL</tt>}

</td>

<td class="docTableCell" align="left" valign="top">

This option specifies which CPU the statistics should be gathered from. If this isn't specified, the system totals are reported.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-q</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This reports information about the run queues and load averages of the machine.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-u</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This reports information about CPU utilization of the system. (This is the default output.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-w</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This reports the number of context switches that occurred in the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-o filename</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This specifies the name of the binary output file that will store the performance statistics.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-f filename</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This specifies the filename of the performance statistics.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The amount of time to wait between samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>count</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total number of samples to record.

</td>

</tr>

</tbody>

</table>

<tt>sar</tt> offers a similar set (with different names) of the system-wide CPU performance statistics that we have seen in the proceeding tools. The list is shown in <a name="iddle0310"></a><a name="iddle0311"></a><a name="iddle0312"></a><a name="iddle0313"></a>[Table 2-17](ch02lev1sec2.html#ch02table17).

<a name="ch02table17"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-17\. <span class="docEmphasis"><tt>sar</tt></span> CPU Statistics

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0314"></a><a name="iddle0315"></a><a name="iddle0316"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>user</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of user time that the CPU has spent during the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>nice</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample running low-priority (or nice) processes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>system</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of system time that the CPU has spent during the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>iowait</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU has spent during the previous sample waiting on I/O.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>idle</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the percentage of time that the CPU was idle during the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>runq-sz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the size of the run queue when the sample was taken.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>plist-sz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of processes present (running, sleeping, or waiting for I/O) when the sample was taken.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ldavg-1</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This was the load average for the last minute.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ldavg-5</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This was the load average for the past 5 minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ldavg-15</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This was the load average for the past 15 minutes.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>proc/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of new processes created per second. (This is the same as the <tt>forks</tt> statistic from <tt>vmstat</tt>.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>cswch</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the number of context switches per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>intr/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of interrupts fired per second.

</td>

</tr>

</tbody>

</table>

One of the significant benefits of <tt>sar</tt> is that it enables you to save many different types of time-stamped system data to log files for later retrieval and review. This can prove very handy when trying to figure out why a particular machine is failing at a particular <a name="iddle0317"></a><a name="iddle0318"></a><a name="iddle0319"></a>time.

<a name="ch02lev3sec14"></a>

##### 2.2.7.2 Example Usage

This first <a name="iddle0320"></a><a name="iddle0321"></a><a name="iddle0322"></a>command shown in [Listing 2.15](ch02lev1sec2.html#ch02ex15) takes three samples of the CPU every second, and stores the results in the binary file <tt>/tmp/apache_test</tt>. This command does not have any visual output and just returns when it has completed.

<a name="ch02ex15"></a>

##### Listing 2.15\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -o /tmp/apache_test 1 3

</pre>

After the information has been stored in the <tt>/tmp/apache_test</tt> file, we can display it in various formats. The default is human readable. This is shown in [Listing 2.16](ch02lev1sec2.html#ch02ex16). This shows similar information to the other system monitoring commands, where we can see how the processor was spending time at a particular <a name="iddle0323"></a><a name="iddle0324"></a><a name="iddle0325"></a>time.

<a name="ch02ex16"></a>

##### Listing 2.16\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -f /tmp/apache_test

Linux 2.4.22-1.2149.nptl (wintermute.phil.org)  03/20/04

17:18:34          CPU     %user     %nice   %system   %iowait      %idle

17:18:35          all     90.00      0.00     10.00      0.00       0.00

17:18:36          all     95.00      0.00      5.00      0.00       0.00

17:18:37          all     92.00      0.00      6.00      0.00       2.00

Average:          all     92.33      0.00      7.00      0.00       0.67

</pre>

However, <tt>sar</tt> can also output the statistics in a format that can be easily imported into a relational database, as shown in [Listing 2.17](ch02lev1sec2.html#ch02ex17). This can be useful for storing a large amount of performance data. Once it has been imported into a relational database, the performance data can be analyzed with all of the tools of a relational database.

<a name="ch02ex17"></a>

##### Listing 2.17\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -f /tmp/apache_test  -H

wintermute.phil.org;1;2004-03-20 22:18:35 UTC;-1;90.00;0.00;10.00;0.00;0.00

wintermute.phil.org;1;2004-03-20 22:18:36 UTC;-1;95.00;0.00;5.00;0.00;0.00

wintermute.phil.org;1;2004-03-20 22:18:37 UTC;-1;92.00;0.00;6.00;0.00;2.00

</pre>

Finally, <tt>sar</tt> can also output the statistics in a format that can be easily parsed by standard Linux tools such as <tt>awk, perl, python</tt>, or <tt>grep</tt>. This output, which is shown in [Listing 2.18](ch02lev1sec2.html#ch02ex18), can be fed into a script that will pull out interesting events, and possibly even analyze different trends in the data.

<a name="ch02ex18"></a>

##### Listing 2.18\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -f /tmp/apache_test  -h

wintermute.phil.org     1       1079821115      all     %user   90.00

wintermute.phil.org     1       1079821115      all     %nice   0.00

wintermute.phil.org     1       1079821115      all     %system 10.00

wintermute.phil.org     1       1079821115      all     %iowait 0.00

wintermute.phil.org     1       1079821115      all     %idle   0.00

wintermute.phil.org     1       1079821116      all     %user   95.00

wintermute.phil.org     1       1079821116      all     %nice   0.00

wintermute.phil.org     1       1079821116      all     %system 5.00

wintermute.phil.org     1       1079821116      all     %iowait 0.00

wintermute.phil.org     1       1079821116      all     %idle   0.00

wintermute.phil.org     1       1079821117      all     %user   92.00

wintermute.phil.org     1       1079821117      all     %nice   0.00

wintermute.phil.org     1       1079821117      all     %system 6.00

wintermute.phil.org     1       1079821117      all     %iowait 0.00

wintermute.phil.org     1       1079821117      all     %idle   2.00

</pre>

In addition to <a name="iddle0326"></a><a name="iddle0327"></a><a name="iddle0328"></a>recording information in a file, <tt>sar</tt> can also be used to observe a system in real time. In the example shown in [Listing 2.19](ch02lev1sec2.html#ch02ex19), the CPU state is sampled three times with one second between them.

<a name="ch02ex19"></a>

##### Listing 2.19\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar 1 3

Linux 2.4.22-1.2149.nptl (wintermute.phil.org)  03/20/04

17:27:10          CPU     %user     %nice   %system   %iowait      %idle

17:27:11          all     96.00      0.00      4.00      0.00       0.00

17:27:12          all     98.00      0.00      2.00      0.00       0.00

17:27:13          all     92.00      0.00      8.00      0.00       0.00

Average:          all     95.33      0.00      4.67      0.00       0.00

</pre>

The default display's purpose is to show information about the CPU, but other information can also be displayed. For example, <tt>sar</tt> can show the number of context switches per second, and the number of memory pages that have been swapped in or out. In [Listing 2.20](ch02lev1sec2.html#ch02ex20), <tt>sar</tt> samples the information two times, with one second between them. In this case, we ask <tt>sar</tt> to show us the total number of context switches and process creations that occur every second. We also ask <tt>sar</tt> for information about the load average. We can see in this example that this machine has 163 process that are in memory but not running. For the past minute, on average 1.12 processes have been ready to <a name="iddle0329"></a><a name="iddle0330"></a><a name="iddle0331"></a>run.

<a name="ch02ex20"></a>

##### Listing 2.20\.

<pre>[ezolt@scrffy manuscript]$ sar -w -c -q 1 2

Linux 2.6.8-1.521smp (scrffy)   10/20/2004

08:23:29 PM    proc/s

08:23:30 PM      0.00

08:23:29 PM   cswch/s

08:23:30 PM    594.00

08:23:29 PM   runq-sz  plist-sz   ldavg-1    ldavg-5  ldavg-15

08:23:30 PM         0       163      1.12       1.17      1.17

08:23:30 PM    proc/s

08:23:31 PM      0.00

08:23:30 PM   cswch/s

08:23:31 PM    812.87

08:23:30 PM   runq-sz  plist-sz   ldavg-1    ldavg-5  ldavg-15

08:23:31 PM         0       163      1.12       1.17      1.17

Average:       proc/s

Average:         0.00

Average:      cswch/s

Average:       703.98

Average:      runq-sz  plist-sz   ldavg-1    ldavg-5  ldavg-15

Average:            0       163      1.12       1.17      1.17

</pre>

As you can see, <tt>sar</tt> is a powerful tool that can record many different performance statistics. It provides a Linux-friendly interface that enables you to easily extract and analyze the performance <a name="iddle0332"></a><a name="iddle0333"></a><a name="iddle0334"></a>data.

<a name="ch02lev2sec12"></a>

#### 2.2.8\. oprofile

<tt>oprofile</tt> is a <a name="iddle0335"></a><a name="iddle0336"></a><a name="iddle0337"></a>performance suite that uses the performance counter hardware available in nearly all modern processors to track where CPU time is being spent on an entire system, and individual processes. In addition to measuring where CPU cycles are spent, <tt>oprofile</tt> can measure very low-level information about how the CPU is performing. Depending on the events supported by the underlying processor, it can measure such things as cache misses, branch mispredictions and memory references, and floating-point operations.

<tt>oprofile</tt> does not record every event that occurs; instead, it works with the processor's performance hardware to sample every <tt>count</tt> events, where <tt>count</tt> is a value that users specify when they start <tt>oprofile</tt>. The lower the value of <tt>count</tt>, the more accurate the results are, but the higher the overhead of <tt>oprofile</tt>. By keeping <tt>count</tt> to a reasonable value, <tt>oprofile</tt> can run with a very low overhead but still give an amazingly accurate account of the performance of the system.

Sampling is very powerful, but be careful for some nonobvious gotchas when using it. First, sampling may say that you are spending 90 percent of your time in a particular routine, but it does not say why. There can be two possible causes for a high number of cycles attributed to a particular routine. First, it is possible that this routine is the bottleneck and is taking a long amount of time to execute. However, it may also be that the function is taking a reasonable amount of time to execute, but is called a large number of times. You can usually figure out which is the case by looking at the samples around, the particularly hot line, or by instrumenting the code to count the number of calls that are made to it.

The second problem of sampling is that you are never quite sure where a function is being called from. Even if you figure out that the function is being called many times and you track down all of the functions that call it, it is not necessarily clear which function is doing the majority of the <a name="iddle0338"></a><a name="iddle0339"></a><a name="iddle0340"></a>calling.

<a name="ch02lev3sec15"></a>

##### 2.2.8.1 CPU Performance-Related Options

<tt>oprofile</tt> <a name="iddle0341"></a><a name="iddle0342"></a><a name="iddle0343"></a>is actually a suite of pieces that work together to collect CPU performance statistics. There are three main pieces of <tt>oprofile</tt>:

*   The <tt>oprofile</tt> kernel module manipulates the processor and turns on and off sampling.

*   The <tt>oprofile</tt> daemon collects the samples and saves them to disk.

*   The <tt>oprofile</tt> reporting tools take the collected samples and show the user how they relate to the applications running on the system.

The <tt>oprofile</tt> suite hides the driver and daemon manipulation in the <tt>opcontrol</tt> command. The <tt>opcontrol</tt> command is used to select which events the processor will sample and start the sampling.

When controlling the daemon, you can invoke <tt>opcontrol</tt> using the following command line:<a name="iddle0344"></a><a name="iddle0345"></a><a name="iddle0346"></a>

<pre>opcontrol [--start] [--stop] [--dump]

</pre>

This option's control, the profiling daemon, enables you to start and stop sampling and to dump the samples from the daemon's memory to disk. When sampling, the <tt>oprofile</tt> daemon stores a large amount of samples in internal buffers. However, it is only possibly to analyze the samples that have been written (or dumped) to disk. Writing to disk can be an expensive operation, so <tt>oprofile</tt> only does it periodically. As a result, after running a test and profiling with <tt>oprofile</tt>, the results may not be available immediately, and you will have to wait until the daemon flushes the buffers to disk. This can be very annoying when you want to begin analysis immediately, so the <tt>opcontrol</tt> command enables you to force the dump of samples from the <tt>oprofile</tt> daemon's internal buffers to disk. This enables you to begin a performance investigation immediately after <a name="iddle0347"></a><a name="iddle0348"></a><a name="iddle0349"></a>a test has completed.

[Table 2-18](ch02lev1sec2.html#ch02table18) describes the <a name="iddle0350"></a><a name="iddle0351"></a><a name="iddle0352"></a><a name="iddle0353"></a>command-line options for the <tt>opcontrol</tt> program that enable you to control the operation of the daemon.

<a name="ch02table18"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-18\. <span class="docEmphasis"><tt>opcontrol</tt></span> Daemon Control

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

<tt>-s/--start</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Starts profiling unless this uses a default event for the current processor

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d/--dump</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Dumps the sampling information that is currently in the kernel sample buffers to the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--stop</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This will stop the profiling.

</td>

</tr>

</tbody>

</table>

By default, <tt>oprofile</tt> picks an event with a given frequency that is reasonable for the processor and kernel that you are running it on. However, it has many more events that can be monitored than the default. When you are listing and selecting an event, <tt>opcontrol</tt> is invoked using the <a name="iddle0354"></a><a name="iddle0355"></a><a name="iddle0356"></a><a name="iddle0357"></a>following command line:

<pre>opcontrol [--list-events] [-event=:name:count:unitmask:kernel:user:]

</pre>

The event <a name="iddle0358"></a><a name="iddle0359"></a><a name="iddle0360"></a><a name="iddle0361"></a>specifier enables you to select which event is going to be sampled; how frequently it will be sampled; and whether that sampling will take place in kernel space, user space, or both. [Table 2-19](ch02lev1sec2.html#ch02table19) describes the command-line option of <tt>opcontrol</tt> that enables you to select different events to sample.

<a name="ch02table19"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-19\. <span class="docEmphasis"><tt>opcontrol</tt></span> Event Handling

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle0362"></a><a name="iddle0363"></a><a name="iddle0364"></a><a name="iddle0365"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-l/--list-events</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Lists the different events that the processor can sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-event=:name:count: unitmask:kernel:user:</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Used to specify what events will be sampled. The event name must be one of the events that the processor supports. A valid event can be retrieved from the <tt>--list- events</tt> option. The <tt>count</tt> parameter specifies that the processor will be sampled every <tt>count</tt> times that event happens. The <tt>unitmask</tt> modifies what the event is going to sample. For example, if you are sampling "reads from memory," the unit mask may allow you to select only those reads that didn't hit in the cache. The <tt>kernel</tt> parameter specifies whether <tt>oprofile</tt> should sample when the processor is running in kernel space. The <tt>user</tt> parameter specifies whether <tt>oprofile</tt> should sample when the processor is running in user space.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--vmlinux = kernel</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Specifies which uncompressed kernel image <tt>oprofile</tt> will use to attribute samples to various kernel functions.

</td>

</tr>

</tbody>

</table>

After the samples have <a name="iddle0366"></a><a name="iddle0367"></a><a name="iddle0368"></a><a name="iddle0369"></a>been collected and saved to disk, <tt>oprofile</tt> provides a different tool, <tt>opreport</tt>, which enables you to view the samples that have been collected. <tt>opreport</tt> is invoked using the following command line:

<pre>opreport [-r] [-t]

</pre>

Typically, <tt>opreport</tt> displays all the samples collected by the system and which executables (including the kernel) are responsible for them. The executables with the highest number of samples are shown first, and are followed by all the executables with samples. In a typical system, most of the samples are in a handful of executables at the top of the list, with a very large number of executables contributing a very small number of samples. To deal with this, <tt>opreport</tt> enables you to set a threshold, and only executables with that percentage of the total samples or greater will be shown. Alternatively, <tt>opreport</tt> can reverse the order of the executables that are shown, so those with a high contribution are shown last. This way, the most important data is printed last, and it will not scroll off the screen.

[Table 2-20](ch02lev1sec2.html#ch02table20) describes these command-line options of <tt>opreport</tt> that enable you to format the output of the <a name="iddle0370"></a><a name="iddle0371"></a><a name="iddle0372"></a><a name="iddle0373"></a>sampling.

<a name="ch02table20"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 2-20\. <span class="docEmphasis"><tt>opreport</tt></span> Report Format

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

<tt>--reverse-sort / -r</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Reverses the order of the sort. Typically, the images that caused the most events display first.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--threshold / -t [percentage]</tt>

</td>

<td class="docTableCell" align="left" valign="top">

Causes <tt>opreport</tt> to only show images that have contributed <tt>percentage</tt> or more amount of samples. This can be useful when there are many images with a very small number of samples and you are only interested in the most significant.

</td>

</tr>

</tbody>

</table>

Again, <tt>oprofile</tt> is a complicated tool, and these options show only the basics of what <tt>oprofile</tt> can do. You learn more about the capabilities of <tt>oprofile</tt> in later <a name="iddle0374"></a><a name="iddle0375"></a><a name="iddle0376"></a><a name="iddle0377"></a>chapters.

<a name="ch02lev3sec16"></a>

##### 2.2.8.2 Example Usage

<tt>oprofile</tt> is a very <a name="iddle0378"></a><a name="iddle0379"></a><a name="iddle0380"></a>powerful tool, but it can also be difficult to install. [Appendix B](app02.html#app02), "[Installing oprofile](app02.html#app02)," contains instructions on how to get <tt>oprofile</tt> installed and running on a few of the major Linux distributions.

We begin the use of <tt>oprofile</tt> by setting it up for profiling. This first command, shown in [Listing 2.21](ch02lev1sec2.html#ch02ex21), uses the <tt>opcontrol</tt> <a name="iddle0381"></a>command to tell the <tt>oprofile</tt> suite where an uncompressed image of the kernel is located. <tt>oprofile</tt> needs to know the location of this file so that it can attribute samples to exact functions within the kernel.

<a name="ch02ex21"></a>

##### Listing 2.21\.

<pre>[root@wintermute root]# opcontrol --vmlinux=/boot/vmlinux-\

2.4.22-1.2174.nptlsmp

</pre>

After we set up the path to the current kernel, we can begin profiling. The command in [Listing 2.22](ch02lev1sec2.html#ch02ex22) tells <tt>oprofile</tt> to start sampling using the default event. This event varies depending on the processor, but the default event for this processor is <tt>CPU_CLK_UNHALTED</tt>. This event samples all of the CPU cycles where the processor is not halted. The 233869 means that the processor will sample the instruction the processor is executing every 233,869 <a name="iddle0382"></a><a name="iddle0383"></a><a name="iddle0384"></a>events.

<a name="ch02ex22"></a>

##### Listing 2.22\.

<pre>[root@wintermute root]# opcontrol -s

Using default event: CPU_CLK_UNHALTED:233869:0:1:1

Using log file /var/lib/oprofile/oprofiled.log

Daemon started.

Profiler running.

</pre>

Now that we have started sampling, we want to begin to analyze the sampling results. In [Listing 2.23](ch02lev1sec2.html#ch02ex23), we start to use the reporting tools to figure out what is happening in the system. <tt>opreport</tt> <a name="iddle0385"></a>reports what has been profiled so far.

<a name="ch02ex23"></a>

##### Listing 2.23\.

<pre>[root@wintermute root]# opreport

opreport op_fatal_error:

No sample file found: try running opcontrol --dump

or specify a session containing sample files

</pre>

Uh oh! Even though the profiling has been happening for a little while, we are stopped when <tt>opreport</tt> <a name="iddle0386"></a>specifies that it cannot find any samples. This is because the <tt>opreport</tt> command is looking for the samples on disk, but the <tt>oprofile</tt> daemon stores the samples in memory and only periodically dumps them to disk. When we ask <tt>opreport</tt> <a name="iddle0387"></a>for a list of the samples, it does not find any on disk and reports that it cannot find any samples. To alleviate this problem, we can force the daemon to flush the samples immediately by issuing a <tt>dump</tt> option to <a name="iddle0388"></a><tt>opcontrol</tt>, as shown in [Listing 2.24](ch02lev1sec2.html#ch02ex24). This command enables us to view the samples that have been <a name="iddle0389"></a><a name="iddle0390"></a><a name="iddle0391"></a>collected.

<a name="ch02ex24"></a>

##### Listing 2.24\.

<pre>[root@wintermute root]# opcontrol --dump

</pre>

After we <tt>dump</tt> the samples to disk, we try again, and ask <tt>oprofile</tt> for the report, as shown in [Listing 2.25](ch02lev1sec2.html#ch02ex25). This time, we have results. The report contains information about the processor that it was collected on and the types of events that were monitored. The report then lists in descending order the number of events that occurred and which executable they occurred in. We can see that the Linux kernel is taking up 50 percent of the total cycles, emacs is taking 14 percent, and libc is taking 12 percent. It is possible to dig deeper into executable and determine which function is taking up all the time, but that is covered in [Chapter 4](ch04.html#ch04), "[Performance Tools: Process-Specific CPU](ch04.html#ch04)."

<a name="ch02ex25"></a>

##### Listing 2.25\.

<pre>[root@wintermute root]# opreport

CPU: PIII, speed 467.739 MHz (estimated)

Counted CPU_CLK_UNHALTED events (clocks processor is not halted)

with a unit mask of 0x00 (No unit mask) count 233869

     3190 50.4507 vmlinux-2.4.22-1.2174.nptlsmp

      905 14.3128 emacs

      749 11.8456 libc-2.3.2.so

      261  4.1278 ld-2.3.2.so

      244  3.8589 mpg321

      233  3.6850 insmod

      171  2.7044 libperl.so

      128  2.0244 bash

      113  1.7871 ext3.o

  ....

</pre>

When we started the <tt>oprofile</tt>, we just used the default event that <tt>opcontrol</tt> chose for us. Each processor has a very rich set of events that can be monitored. In [Listing 2.26](ch02lev1sec2.html#ch02ex26), we ask <tt>opcontrol</tt> <a name="iddle0392"></a>to list all the events that are available for this particular CPU. This list is quite long, but in this case, we can see that in addition to <tt>CPU_CLK_UNHALTED</tt>, we can also monitor <tt>DATA_MEM_REFS</tt> and <tt>DCU_LINES_IN</tt>. These are memory events caused by the memory subsystem, and we investigate them in later <a name="iddle0393"></a><a name="iddle0394"></a><a name="iddle0395"></a>chapters.

<a name="ch02ex26"></a>

##### Listing 2.26\.

<pre>[root@wintermute root]# opcontrol -l

oprofile: available events for CPU type "PIII"

See Intel Architecture Developer's Manual Volume 3, Appendix A and

Intel Architecture Optimization Reference Manual (730795-001)

CPU_CLK_UNHALTED: (counter: 0, 1)

        clocks processor is not halted (min count: 6000)

DATA_MEM_REFS: (counter: 0, 1)

        all memory references, cachable and non (min count: 500)

DCU_LINES_IN: (counter: 0, 1)

        total lines allocated in the DCU (min count: 500)

....

</pre>

The command needed to specify which events we will monitor can be cumbersome, so fortunately, we can also use <tt>oprofile</tt>'s graphical <tt>oprof_start</tt> command to graphically start and stop sampling. This enables us to select the events that we want graphically without the need to figure out the exact way to specify on the command line the events that we want to monitor.

In the example of <tt>op_control</tt> shown in [Figure 2-3](ch02lev1sec2.html#ch02fig03), we tell <tt>oprofile</tt> that we want to monitor <tt>DATA_MEM_REFS</tt> and <tt>L2_LD</tt> events at the same time. The <tt>DATA_MEM_REFS</tt> event can tell us which applications use the memory subsystem a lot and which use the level 2 cache. In this particular processor, the processor's hardware has only two counters that can be used for sampling, so only two events can be used simultaneously.

<a name="ch02fig03"></a>

<center>

##### Figure 2-3\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/02fig03_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/02fig03_alt.jpg)

[Now that we have gathered the samples using the graphical interface to <tt>operofile</tt>, we can now analyze the data that it has collected. In](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/02fig03_alt.jpg) [Listing 2.27](ch02lev1sec2.html#ch02ex27), we ask <tt>opreport</tt> to display the profile of samples that it has collected in a similar way to how we did when we were monitoring cycles. In this case, we can see that the libmad library has 31 percent of the data memory references of the whole system and appears to be the heaviest user of <a name="iddle0396"></a><a name="iddle0397"></a><a name="iddle0398"></a>the memory subsystem.

<a name="ch02ex27"></a>

##### Listing 2.27\.

<pre>[root@wintermute root]# opreport

CPU: PIII, speed 467.739 MHz (estimated)

Counted DATA_MEM_REFS events (all memory references, cachable and non)

with a unit mask of 0x00 (No unit mask) count 30000

Counted L2_LD events (number of L2 data loads) with a unit mask of 0x0f

(All cache states) count 233869

    87462 31.7907        17  3.8636 libmad.so.0.1.0

    24259  8.8177        10  2.2727 mpg321

    23735  8.6272        40  9.0909 libz.so.1.2.0.7

    17513  6.3656        56 12.7273 libgklayout.so

    17128  6.2257        90 20.4545 vmlinux-2.4.22-1.2174.nptlsmp

    13471  4.8964         4  0.9091 libpng12.so.0.1.2.2

    12868  4.6773        20  4.5455 libc-2.3.2.so

....

</pre>

The output provided by <tt>opreport</tt> <a name="iddle0399"></a>displays all the system libraries and executables that contain any of the events that we were sampling. Note that not all the events have been recorded; because we are sampling, only a subset of events are actually recorded. This is usually not a problem, because if a particular library or executable is a performance problem, it will likely cause high-cost events to happen many times. If the sampling is random, these high-cost events will eventually be caught by the <a name="iddle0400"></a><a name="iddle0401"></a><a name="iddle0402"></a>sampling code.