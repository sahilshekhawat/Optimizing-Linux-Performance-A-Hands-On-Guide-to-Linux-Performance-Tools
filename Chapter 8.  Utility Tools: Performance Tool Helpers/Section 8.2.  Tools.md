### 8.2\. Tools

Used together, the following tools can greatly enhance the effectiveness and ease of use of the performance tools described in previous chapters.

<a name="ch08lev2sec5"></a>

#### 8.2.1\. bash

<tt>bash</tt> is the default <a name="iddle1953"></a><a name="iddle1954"></a>Linux command-line shell, and you most likely use it every time you interact with the Linux <a name="iddle1955"></a><a name="iddle1956"></a>command line. <tt>bash</tt> has a powerful scripting language that is typically used to create shell scripts. However, the scripting language can also be called from the command line and enables you to easily automate some of the more tedious tasks during a performance investigation.

<a name="ch08lev3sec1"></a>

##### 8.2.1.1 Performance-Related Options

<tt>bash</tt> provides a series of commands that can be used together to periodically run a particular command. Most Linux users have <tt>bash</tt> as their default shell, so just logging in to a machine or opening a terminal brings up a <tt>bash</tt> prompt. If you are not using <tt>bash</tt>, you can invoke it by typing <tt>bash</tt>.

After you have a <tt>bash</tt> command prompt, you can enter a series of <tt>bash</tt> scripting commands to automate the continuous execution of a particular command. This feature proves most useful when you need to periodically extract performance statistics using a particular command. These scripting options are described <a name="iddle1957"></a><a name="iddle1958"></a><a name="iddle1959"></a><a name="iddle1960"></a>in [Table 8-1](ch08lev1sec2.html#ch08table01).

<a name="ch08table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 8-1\. <span class="docEmphasis"><tt>bash</tt></span> Runtime Scripting Options

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

<tt>while condition</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1961"></a>This executes a loop until the condition is false.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>do</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1962"></a>This indicates the start of a loop.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>done</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1963"></a>This indicates the end of a loop.

</td>

</tr>

</tbody>

</table>

<tt>bash</tt> is infinitely flexible and is documented in the <tt>bash</tt> man page. Although <tt>bash</tt>'s complexity can be overwhelming, it is not necessary to master it all to put <tt>bash</tt> immediately to <a name="iddle1964"></a><a name="iddle1965"></a><a name="iddle1966"></a><a name="iddle1967"></a>use.

<a name="ch08lev3sec2"></a>

##### 8.2.1.2 Example Usage

Although some <a name="iddle1968"></a><a name="iddle1969"></a>performance tools, such as <tt>vmstat</tt> and <tt>sar</tt>, periodically display updated performance statistics, other commands, such as <tt>ps</tt> and <tt>ifconfig</tt>, do not. <tt>bash</tt> can call commands such as <tt>ps</tt> and <tt>ifconfig</tt> to periodically display their statistics. For example, in [Listing 8.1](ch08lev1sec2.html#ch08ex01), we ask <tt>bash</tt> to do something in a <tt>while</tt> loop based on the condition <tt>TRue</tt>. Because the <tt>TRue</tt> command is always true, the <tt>while</tt> loop will never exit. Next, the commands that will be executed after each iteration start after the <tt>do</tt> command. These commands ask <tt>bash</tt> to sleep for one second and then run <tt>ifconfig</tt> to extract performance information about the <tt>eth0</tt> controller. However, because we are only interested in the received packets, we <tt>grep</tt> output of <tt>ifconfig</tt> for the string <tt>"RX packets"</tt>. Finally, we issue the <tt>done</tt> command to tell <tt>bash</tt> we are done with the loop. Because the <tt>TRue</tt> command always returns true, this entire loop will run forever unless we interrupt it <a name="iddle1970"></a><a name="iddle1971"></a><a name="iddle1972"></a><a name="iddle1973"></a>with a <Ctrl-C>.

<a name="ch08ex01"></a>

##### Listing 8.1\.

<pre>[ezolt@wintermute tmp]$ while true; do sleep 1; /sbin/ifconfig eth0 | grep

"RX packets" ; done;

                         RX packets:2256178 errors:0 dropped:0 overruns:0 frame:0

                         RX packets:2256261 errors:0 dropped:0 overruns:0 frame:0

                         RX packets:2256329 errors:0 dropped:0 overruns:0 frame:0

                         RX packets:2256415 errors:0 dropped:0 overruns:0 frame:0

                         RX packets:2256459 errors:0 dropped:0 overruns:0 frame:0

...

</pre>

With the bash script in [Listing 8.1](ch08lev1sec2.html#ch08ex01), you see network performance statistics updated every second. The same loop can be used to monitor other events by changing the <tt>ifconfig</tt> command to some other command, and the amount of time between updates can also be varied by changing the amount of sleep. This simple loop is easy to type directly into the command line and enables you to automate the display of any performance statistics that interest <a name="iddle1974"></a><a name="iddle1975"></a><a name="iddle1976"></a><a name="iddle1977"></a>you.

<a name="ch08lev2sec6"></a>

#### 8.2.2\. tee

<tt>tee</tt> <a name="iddle1978"></a><a name="iddle1979"></a>is a simple <a name="iddle1980"></a><a name="iddle1981"></a>command that enables you to simultaneously save the standard output of a command to a file and display it. <tt>tee</tt> also proves useful when you want to save a performance tool's output and view it at the same time, such as when you are monitoring the performance statistics of a live system, but also storing them for later analysis.

<a name="ch08lev3sec3"></a>

##### 8.2.2.1 Performance-Related Options

<tt>tee</tt> is invoked with the following command line:

<pre><command> | tee [-a] [file]

</pre>

<tt>tee</tt> takes the output provided by <tt><command></tt> and saves it to the specified file, but also prints it to standard output. If the <tt>-a</tt> option is specified, <tt>tee</tt> appends <a name="iddle1982"></a><a name="iddle1983"></a><a name="iddle1984"></a><a name="iddle1985"></a>the output to the file instead of overwriting it.

<a name="ch08lev3sec4"></a>

##### 8.2.2.2 Example Usage

[Listing 8.2](ch08lev1sec2.html#ch08ex02) shows <a name="iddle1986"></a><a name="iddle1987"></a><tt>tee</tt> being used to record the output of <tt>vmstat</tt>. As you can see, <tt>tee</tt> displays the output that <tt>vmstat</tt> has generated, but it also saves it in the file <tt>/tmp/vmstat_out</tt>. Saving the output of <tt>vmstat</tt> enables us to analyze or graph the performance data at a later date.

<a name="ch08ex02"></a>

##### Listing 8.2\.

<pre>[ezolt@localhost book]$ vmstat 1 5 | tee /tmp/vmstat_out

procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   swpd   free   buff  cache   si   so    bi    bo   in    cs us sy id wa

 2  0 135832   3648  16112  95236    2    3    15    14   39   194  3  1 92  4

 0  0 135832   4480  16112  95236    0    0     0     0 1007  1014  7  2 91  0

 1  0 135832   4480  16112  95236    0    0     0     0 1002   783  6  2 92  0

 0  0 135832   4480  16112  95236    0    0     0     0 1005   828  5  2 93  0

 0  0 135832   4480  16112  95236    0    0     0     0 1056   920  7  3 90  0

</pre>

<tt>tee</tt> is a simple command, but it is powerful because it makes it easy to record the output of a given performance <a name="iddle1988"></a><a name="iddle1989"></a><a name="iddle1990"></a><a name="iddle1991"></a>tool.

<a name="ch08lev2sec7"></a>

#### 8.2.3\. script

The <a name="iddle1992"></a><a name="iddle1993"></a><tt>script</tt> command is <a name="iddle1994"></a><a name="iddle1995"></a>used to save all the input and output generated during a shell session into a text file. This text file can be used later to both replay the executed commands and review the results. When investigating a performance problem, it is useful to have a record of the exact command lines executed so that you can later review the exact tests you performed. Having a record of the executed commands means that you also can easily cut and paste the command lines when investigating a different problem. In addition, it is useful to have a record of the performance results so that you can review them later when looking for new insights.

<a name="ch08lev3sec5"></a>

##### 8.2.3.1 Performance-Related Options

<tt>script</tt> is a relatively simple command. When run, it just starts a new shell and records all the keystrokes and input and the output generated during the life of the shell into a text file. <tt>script</tt> is invoked with the following command line:

<pre>script [-a] [-t] [file]

</pre>

By default, <tt>script</tt> places all the output into a file called <tt>typescript</tt> unless you specify a different one. [Table 8-2](ch08lev1sec2.html#ch08table02) describes some of the command-line <a name="iddle1996"></a><a name="iddle1997"></a><a name="iddle1998"></a><a name="iddle1999"></a>options of <tt>script</tt>.

<a name="ch08table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 8-2\. <span class="docEmphasis"><tt>script</tt></span> Command-Line Options

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

<tt>-a</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2000"></a>Appends the script output to the file instead of overwriting it.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-t</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2001"></a>Adds timing information about the amount of time between each output/input. This prints the number of characters displayed and the amount of time elapsed between the display of each group of characters.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>file</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2002"></a>Name of the output file.

</td>

</tr>

</tbody>

</table>

One word of warning: <tt>script</tt> literally captures every type of output that was sent to the screen. If you have colored or bold output, this shows up as <tt>esc</tt> characters within the output file. These characters can significantly clutter the output and are not usually useful. If you set the <tt>TERM</tt> environmental variable to <tt>dumb</tt> (using <tt>setenv TERM dumb</tt> for <tt>csh</tt>-based shells and <tt>export TERM=dumb</tt> for <tt>sh</tt>-based shells), applications will not output the escape characters. This provides a more readable output.

In addition, the timing information provided by <tt>script</tt> clutters the output. Although it can be useful to have automatically generated timing information, it may be easier to not use <tt>script</tt>'s timing, and instead just time the important commands with the <tt>time</tt> command mentioned in the previous <a name="iddle2003"></a><a name="iddle2004"></a><a name="iddle2005"></a><a name="iddle2006"></a>chapter.

<a name="ch08lev3sec6"></a>

##### 8.2.3.2 Example Usage

As stated previously, we will have <a name="iddle2007"></a><a name="iddle2008"></a>more readable <tt>script</tt> output if we set the terminal to <tt>dumb</tt>. We can do that with the following command:

<pre>[ezolt@wintermute manuscript]$ export TERM=dumb

</pre>

Next, we actually start the <tt>script</tt> command. [Listing 8.3](ch08lev1sec2.html#ch08ex03) shows <tt>script</tt> being started with an output file of <tt>ps_output</tt>. <tt>script</tt> continues to record the session until you exit the shell with the <tt>exit</tt> command or a <Ctrl-D>.

<a name="ch08ex03"></a>

##### Listing 8.3\.

<pre>

[ezolt@wintermute manuscript]$ script ps_output

Script started, file is ps_output

[ezolt@wintermute manuscript]$ ps

  PID TTY          TIME CMD

 4285 pts/1    00:00:00 bash

 4413 pts/1    00:00:00 ps

[ezolt@wintermute manuscript]$ Script done, file is ps_output

</pre>

Next, in [Listing 8.4](ch08lev1sec2.html#ch08ex04), we look at the output recorded by <tt>script</tt>. As you can see, it contains all the commands and output that we <a name="iddle2009"></a><a name="iddle2010"></a><a name="iddle2011"></a><a name="iddle2012"></a>generated.

<a name="ch08ex04"></a>

##### Listing 8.4\.

<pre>[ezolt@wintermute manuscript]$ cat ps_output

Script started on Wed Jun 16 20:43:35 2004

[ezolt@wintermute manuscript]$ ps

  PID TTY          TIME CMD

 4285 pts/1    00:00:00 bash

 4413 pts/1    00:00:00 ps

[ezolt@wintermute manuscript]$

Script done on Wed Jun 16 20:43:41 2004

</pre>

<tt>script</tt> is a great command to accurately record all interaction during a session. The files that <tt>script</tt> generates are tiny compared to the size of modern hard drives. Recording a performance investigation session and saving it for later review is always a good idea. At worst, it is a small amount of wasted effort and disk space to record the session. At best, the saved sessions can be looked at later and do not require you to rerun the commands recorded in that <a name="iddle2013"></a><a name="iddle2014"></a><a name="iddle2015"></a><a name="iddle2016"></a>session.

<a name="ch08lev2sec8"></a>

#### 8.2.4\. watch

By <a name="iddle2017"></a><a name="iddle2018"></a>default, the <tt>watch</tt> command runs a <a name="iddle2019"></a><a name="iddle2020"></a>command every second and displays its output on the screen. <tt>watch</tt> is useful when working with performance tools that do not periodically display updated results. For example, some tools, such as <tt>ifconfig</tt> and <tt>ps</tt>, display the current performance statistics and then exit. Because <tt>watch</tt> periodically runs these commands and displays their output, it is possible to see by glancing at the screen which statistics are changing and how fast they are changing.

<a name="ch08lev3sec7"></a>

##### 8.2.4.1 Performance-Related Options

<tt>watch</tt> is invoked with the following command line:

<pre>watch [-d[=cumulative]] [-n sec] <command>

</pre>

If called with no parameters, <tt>watch</tt> just displays the output of the given command every second until you interrupt it. In the default output, it can often be difficult to see what has changed from screen to screen, so <tt>watch</tt> provides options that highlight the differences between each output. This can make it easier to spot the differences in output between each sample. [Table 8-3](ch08lev1sec2.html#ch08table03) describes the command-line options that <tt>watch</tt> <a name="iddle2021"></a><a name="iddle2022"></a><a name="iddle2023"></a><a name="iddle2024"></a>accepts.

<a name="ch08table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 8-3\. <span class="docEmphasis"><tt>watch</tt></span> Command-Line Options

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

<tt>-d[=cumulative]</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2025"></a>This option highlights the output that has changed between each sample. If the cumulative option is used, an area is highlighted if it has ever changed, not just if it has changed between samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n sec</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2026"></a>The number of seconds to wait between updates.

</td>

</tr>

</tbody>

</table>

<tt>watch</tt> is a great tool to see how a performance statistic changes over time. It is not a complicated tool, but does its job well. It really fills a void when using performance tools that cannot periodically display updated output. When using these tools, you can run <tt>watch</tt> in a window and glance at it periodically to see how the statistic <a name="iddle2027"></a><a name="iddle2028"></a>changes.

<a name="ch08lev3sec8"></a>

##### 8.2.4.2 Example Usage

The first <a name="iddle2029"></a><a name="iddle2030"></a>example, in [Listing 8.5](ch08lev1sec2.html#ch08ex05), shows <tt>watch</tt> being run with the <tt>ps</tt> command. We are asking <tt>ps</tt> to show us the number of minor faults that each process is generating. <tt>watch</tt> clears the screen and updates this information every 10 seconds. Note that it may be necessary to enclose the command that you want to run in quotation marks so that watch does not confuse the options of the command that you are trying to execute with its own <a name="iddle2031"></a><a name="iddle2032"></a>options.

<a name="ch08ex05"></a>

##### Listing 8.5\.

<pre>[ezolt@wintermute ezolt]$ watch  -n 10 "ps -o minflt,cmd"

Every 10s: ps -o minflt,cmd

Wed Jun 16 08:33:21 2004

MINFLT CMD

  1467 bash

    41 watch -n 1 ps -o minflt,cmd

    66 ps -o minflt,cmd

</pre>

<tt>watch</tt> is a tool whose basic function could easily be written as a simple shell script. However, <tt>watch</tt> is easier than using a shell script because it is almost always available and just works. Remember that performance tools such as <tt>ifconfig</tt> or <tt>ps</tt> display statistics only once, whereas <tt>watch</tt> makes it easier to follow (with only a glance) how the statistics <a name="iddle2033"></a><a name="iddle2034"></a>change.

<a name="ch08lev2sec9"></a>

#### 8.2.5\. gnumeric

When <a name="iddle2035"></a><a name="iddle2036"></a>investigating a performance problem, the <a name="iddle2037"></a><a name="iddle2038"></a>performance tools often generate vast amounts of performance statistics. It can sometimes be problematic to sort through this data and find the trends and patterns that demonstrate how the system is behaving. Spreadsheets in general, and <tt>gnumeric</tt> in particular, provide three different aspects that make this task easier. First, <tt>gnumeric</tt> provides built-in functions, such as max, min, average, and standard deviation, which enable you to numerically analyze the performance data. Second, <tt>gnumeric</tt> provides a flexible way to import the tabular text data commonly output by many performance tools. Finally, <tt>gnumeric</tt> provides a powerful graphing utility that can visualize the performance data generated by the performance tools. This can prove invaluable when searching for data trends over long periods of time. It is also especially useful when looking for correlations between different types of data (such as the correlation between disk I/O and CPU usage). It is often hard to see patterns in text output, but in graphical form, the system's behavior can be much clearer. Other spreadsheets, such as OpenOffice's <tt>oocalc</tt>, could also be used, but <tt>gnumeric</tt>'s powerful text importer and graphing tools make it the easiest to <a name="iddle2039"></a><a name="iddle2040"></a><a name="iddle2041"></a><a name="iddle2042"></a>use.

<a name="ch08lev3sec9"></a>

##### 8.2.5.1 Performance-Related Options

To use a spreadsheet to assist in performance analysis, just follow these steps:

<a name="ch08pro01"></a>

<table border="0" class="docText">

<tbody>

<tr>

<td width="25" valign="top">

<div class="docText">**1\.**</div>

</td>

<td>

<div class="docText">Save performance data into a text file.  

</div>

</td>

</tr>

<tr>

<td width="25" valign="top">

<div class="docText">**2\.**</div>

</td>

<td>

<div class="docText">Import the text file into <tt>gnumeric</tt>.  

</div>

</td>

</tr>

<tr>

<td width="25" valign="top">

<div class="docText">**3\.**</div>

</td>

<td>

<div class="docText">Analyze or graph the data.  

</div>

</td>

</tr>

</tbody>

</table>

<tt>gnumeric</tt> can generate many different types of graphs and has many different functions to analyze data. The best way to see <tt>gnumeric</tt>'s power and flexibility is to load some data and experiment with <a name="iddle2043"></a><a name="iddle2044"></a>it.

<a name="ch08lev3sec10"></a>

##### 8.2.5.2 Example Usage

To demonstrate <a name="iddle2045"></a><a name="iddle2046"></a>the usefulness of the <tt>gnumeric</tt>, we first have to generate performance data that we will graph or analyze. [Listing 8.6](ch08lev1sec2.html#ch08ex06) asks <tt>vmstat</tt> to generate 100 seconds of output and save that information in a text file called <tt>vmstat_output</tt>. This data will be loaded into <tt>gnumeric</tt>. The <tt>-n</tt> option tells <tt>vmstat</tt> to print only header information once (rather than after every screenful of information).

<a name="ch08ex06"></a>

##### Listing 8.6\.

<pre>[ezolt@nohs ezolt]$ vmstat -n 1 100 > vmstat_output

</pre>

Next, we start gnumeric using the following command:

<pre>[ezolt@nohs ezolt]$ gnumeric &

</pre>

This opens a blank spreadsheet where we can import the vmstat data.

Selecting File > Open in <tt>gnumeric</tt> brings up a dialog (not shown) that enables you to select both the file to open and the type of file. We select Text Import (Configurable) for file type, and we are guided through a series of screens to select which columns of the <tt>vmstat_output</tt> file map to which columns of the spreadsheet. For <tt>vmstat</tt>, it is useful to start importing at the second line of text, because the second line contains the names and sizing appropriate for each column. It is also useful to select Fixed-Width for importing the data because that is how <tt>vmstat</tt> outputs its data. After successfully importing the data, we see the spreadsheet <a name="iddle2047"></a><a name="iddle2048"></a><a name="iddle2049"></a><a name="iddle2050"></a>in [Figure 8-1](ch08lev1sec2.html#ch08fig01).

<a name="ch08fig01"></a>

<center>

##### Figure 8-1\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig01_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig01_alt.jpg)

[Next, we graph the data that we have imported. In](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig01_alt.jpg) [Figure 8-2](ch08lev1sec2.html#ch08fig02), we create a stacked graph of the different CPU usages (<tt>us, sys, id, wa</tt>). Because these statistics should always total 100 percent (or close to it), we can see which state dominates at each time. In this case, the system is idle most of the time, but it has a big amount of wait time in the first quarter of the <a name="iddle2051"></a><a name="iddle2052"></a><a name="iddle2053"></a><a name="iddle2054"></a>graph.

<a name="ch08fig02"></a>

<center>

##### Figure 8-2\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig02_alt.jpg)</div>

</center>

[  

Graphs can be a powerful way to see how the performance statistics of a single run of a test change over time. It can also prove useful to see how different runs compare to each other. When graphing data from different runs, be sure to use the same scale for each of the graphs. This allows you to compare and contrast the data more easily.

](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig02_alt.jpg)

[<tt>gnumeric</tt> is a lightweight application that enables you to quickly and easily import and graph/analyze vast amounts of performance data. It is a great tool to play around with performance data to see whether](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/08fig02_alt.jpg) <a name="iddle2055"></a><a name="iddle2056"></a><a name="iddle2057"></a><a name="iddle2058"></a>any interesting characteristics appear.

<a name="ch08lev2sec10"></a>

#### 8.2.6\. ldd

<tt>ldd</tt> <a name="iddle2059"></a><a name="iddle2060"></a>can be used to display which libraries a particular binary relies on. <tt>ldd</tt> helps track down the location of a library <a name="iddle2061"></a><a name="iddle2062"></a><a name="iddle2063"></a>function that an application may be using. By figuring out all the libraries that an application is using, it is possible to search through each of them for the library that contains a given function.

<a name="ch08lev3sec11"></a>

##### 8.2.6.1 Performance-Related Options

<tt>ldd</tt> is invoked with the following command line:

<pre>ldd <binary>

</pre>

<tt>ldd</tt> then displays a list of all the libraries that this binary requires and which files in the system are fulfilling those <a name="iddle2064"></a><a name="iddle2065"></a><a name="iddle2066"></a><a name="iddle2067"></a><a name="iddle2068"></a>requirements.

<a name="ch08lev3sec12"></a>

##### 8.2.6.2 Example Usage

[Listing 8.7](ch08lev1sec2.html#ch08ex07) shows <tt>ldd</tt> being used on the <tt>ls</tt> binary. In this particular case, we can see that <tt>ls</tt> relies on the following libraries: <tt>linux-gate.so.1</tt>, <tt>librt.so.1</tt>, <tt>libacl.so.1</tt>, <tt>libselinux.so.1</tt>, <tt>libc.so.6</tt>, <tt>libpthread.so.0</tt>, <tt>ld-linux.so.2</tt>, and <tt>libattr.so.1</tt>.

<a name="ch08ex07"></a>

##### Listing 8.7\.

<pre>[ezolt@localhost book]$ ldd /bin/ls

        linux-gate.so.1 =>  (0x00dfe000)

        librt.so.1 => /lib/tls/librt.so.1 (0x0205b000)

        libacl.so.1 => /lib/libacl.so.1 (0x04983000)

        libselinux.so.1 => /lib/libselinux.so.1 (0x020c0000)

        libc.so.6 => /lib/tls/libc.so.6 (0x0011a000)

        libpthread.so.0 => /lib/tls/libpthread.so.0 (0x00372000)

        /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00101000)

        libattr.so.1 => /lib/libattr.so.1 (0x03fa4000)

</pre>

<tt>ldd</tt> is a relatively simple tool, but it can be invaluable when trying to track down exactly which libraries an application is using and where <a name="iddle2072"></a><a name="iddle2073"></a><a name="iddle2074"></a><a name="iddle2075"></a><a name="iddle2076"></a>they are located on the system.

<a name="ch08lev2sec11"></a>

#### 8.2.7\. objdump

<tt>objdump</tt> is a <a name="iddle2077"></a><a name="iddle2078"></a>complicated and powerful tool for analyzing various aspects of <a name="iddle2079"></a><a name="iddle2080"></a>binaries or libraries. Although it has many other capabilities, it can be used to determine which functions a given library provides.

<a name="ch08lev3sec13"></a>

##### 8.2.7.1 Performance-Related Options

<tt>objdump</tt> is invoked with the following command line:

<pre>objdump -T <binary>

</pre>

When object is invoked with the <tt>-T</tt> option, it displays all the symbols that this library/binary either relies on or provides. These symbols can be data structures or functions. Every line of the <tt>objdump</tt> output that contains <tt>.text</tt> is a function that <a name="iddle2081"></a><a name="iddle2082"></a>this binary provides.

<a name="ch08lev3sec14"></a>

##### 8.2.7.2 Example Usage

[Listing 8.8](ch08lev1sec2.html#ch08ex08) shows <tt>objdump</tt> used to analyze the <tt>gtk</tt> library. Because we are only interested in the symbols that <tt>libgtk.so</tt> provides, we use <tt>fgrep</tt> to prune the output to only those lines that contain <tt>.text</tt>. In this case, we can see that some of the functions that <tt>libgtk.so</tt> provides are <tt>gtk_arg_values_equal</tt>, <tt>gtk_tooltips_set_colors</tt>, <a name="iddle2085"></a><a name="iddle2086"></a>and <tt>gtk_viewport_set_hadjustment</tt>.

<a name="ch08ex08"></a>

##### Listing 8.8\.

<pre>[ezolt@localhost book]$ objdump -T /usr/lib/libgtk.so | fgrep .text

0384eb60 l    d  .text  00000000

0394c580 g    DF .text  00000209  Base        gtk_arg_values_equal

0389b630 g    DF .text  000001b5  Base        gtk_signal_add_emission_hook_full

0385cdf0 g    DF .text  0000015a  Base        gtk_widget_restore_default_style

03865a20 g    DF .text  000002ae  Base        gtk_viewport_set_hadjustment

03929a20 g    DF .text  00000112  Base        gtk_clist_columns_autosize

0389d9a0 g    DF .text  000001bc  Base        gtk_selection_notify

03909840 g    DF .text  000001a4  Base        gtk_drag_set_icon_pixmap

03871a20 g    DF .text  00000080  Base        gtk_tooltips_set_colors

038e6b40 g    DF .text  00000028  Base        gtk_hseparator_new

038eb720 g    DF .text  0000007a  Base        gtk_hbutton_box_set_layout_default

038e08b0 g    DF .text  000003df  Base        gtk_item_factory_add_foreign

03899bc0 g    DF .text  000001d6  Base        gtk_signal_connect_object_while_alive

....

</pre>

When using performance tools (such as <tt>ltrace</tt>), which display the library functions an application calls (but not the libraries themselves), <tt>objdump</tt> helps locate the shared library each function is present <a name="iddle2087"></a><a name="iddle2088"></a><a name="iddle2089"></a><a name="iddle2090"></a>in.

<a name="ch08lev2sec12"></a>

#### 8.2.8\. GNU Debugger (gdb)

<tt>gdb</tt> is a powerful <a name="iddle2091"></a><a name="iddle2092"></a>application debugger that can help investigate many different aspects of a running <a name="iddle2093"></a><a name="iddle2094"></a><a name="iddle2095"></a>application. <tt>gdb</tt> has three features that make it a valuable tool when diagnosing performance problems. First, <tt>gdb</tt> can attach to a currently running process. Second, <tt>gdb</tt> can display a backtrace for that process, which shows the current source line and the call tree. Attaching to a process and extracting a backtrace can be a quick way to find some of the more obvious performance problems. However, if the application is not stuck in a single location, it may be hard to diagnose the problem using <tt>gdb</tt>, and a system-wide profiler, such as <tt>oprofile</tt>, is a much better choice. Finally, <tt>gdb</tt> can map a virtual address back to a particular function. <tt>gdb</tt> may do a better job of figuring out the location of the virtual address than performance tools. For example, if <tt>oprofile</tt> gives information about where events occur in relation to a virtual address rather than a function name, <tt>gdb</tt> can be used to figure out the function for that address.

<a name="ch08lev3sec15"></a>

##### 8.2.8.1 Performance-Related Options

<tt>gdb</tt> is invoked with the <a name="iddle2096"></a><a name="iddle2097"></a><a name="iddle2098"></a><a name="iddle2099"></a><a name="iddle2100"></a>following command line, in which <tt>pid</tt> is the process that <tt>gdb</tt> will attach to:

<pre>gdb -p pid

</pre>

After <tt>gdb</tt> has attached to the process, it enters an interactive mode in which you can examine the current execution location and runtime variables for the given process. [Table 8-4](ch08lev1sec2.html#ch08table04) describes one of the commands that you can use to examine <a name="iddle2101"></a><a name="iddle2102"></a>the running process.

<a name="ch08table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 8-4\. <span class="docEmphasis"><tt>gdb</tt></span> Runtime Options

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

<tt>bt</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2103"></a>This shows the backtrace for the currently executing process.

</td>

</tr>

</tbody>

</table>

<tt>gdb</tt> has many more command-line options and runtime controls that are more appropriate for debugging rather than a performance investigation. See the <tt>gdb</tt> man page or type <tt>help</tt> at the <tt>gdb</tt> prompt for more <a name="iddle2104"></a><a name="iddle2105"></a><a name="iddle2106"></a>information.

<a name="ch08lev3sec16"></a>

##### 8.2.8.2 Example Usage

To examine <a name="iddle2107"></a><a name="iddle2108"></a><a name="iddle2109"></a>how <tt>gdb</tt> works, it is useful to demonstrate it on a simple test application. The program in [Listing 8.9](ch08lev1sec2.html#ch08ex09) just calls function <tt>a()</tt> from <tt>main</tt> and spins in an infinite loop. The program will never exit, so when we attach to it with <tt>gdb</tt>, it should always be executing the infinite loop in function <a name="iddle2110"></a><a name="iddle2111"></a><tt>a()</tt>.

<a name="ch08ex09"></a>

##### Listing 8.9\.

<pre>void a(void)

{

  while(1);

}

main()

{

  a();

}

</pre>

[Listing 8.10](ch08lev1sec2.html#ch08ex10) launches the application and attaches to its <tt>pid</tt> with <tt>gdb</tt>. We ask gdb to generate a backtrace, which shows us exactly what code is currently executing and, what set of function calls leads to the current location. As expected, <tt>gdb</tt> shows us that we were executing the infinite loop in <tt>a()</tt>, and that this was <a name="iddle2112"></a><a name="iddle2113"></a><a name="iddle2114"></a><a name="iddle2115"></a><a name="iddle2116"></a>called from <tt>main()</tt>.

<a name="ch08ex10"></a>

##### Listing 8.10\.

<pre>[ezolt@wintermute examples]$ ./chew &

[2] 17389

[ezolt@wintermute examples]$ gdb -p 17389

GNU gdb Red Hat Linux (5.3.90-0.20030710.41rh)

Copyright 2003 Free Software Foundation, Inc.

GDB is free software, covered by the GNU General Public License, and you are

welcome to change it and/or distribute copies of it under certain conditions.

Type "show copying" to see the conditions.

There is absolutely no warranty for GDB. Type "show warranty" for details.

This GDB was configured as "i386-redhat-linux-gnu".

Attaching to process 17389

Reading symbols from /usr/src/perf/utils/examples/chew...done.

Using host libthread_db library

"/lib/tls/libthread_db.so.1".

Reading symbols from /lib/tls/libc.so.6...done.

Loaded symbols for /lib/tls/libc.so.6

Reading symbols from /lib/ld-linux.so.2...done.

Loaded symbols for /lib/ld-linux.so.2

a () at chew.c:3

3         while(1);

<span class="docEmphStrong">(gdb) bt

#0  a () at chew.c:3

#1  0x0804832f in main () at chew.c:8</span>

</pre>

Finally, in [Listing 8.11](ch08lev1sec2.html#ch08ex11), we ask gdb to show us where the virtual address 0x0804832F is located, and gdb shows that that address is part of the function <a name="iddle2117"></a><a name="iddle2118"></a><a name="iddle2119"></a><a name="iddle2120"></a><a name="iddle2121"></a>main.

<a name="ch08ex11"></a>

##### Listing 8.11\.

<pre>(gdb) x 0x0804832f

0x804832f <main+21>: 0x9090c3c9

</pre>

<tt>gdb</tt> is an extraordinarily powerful debugger and can be helpful during a performance investigation. It is even helpful after the performance problem has been identified, when you need to determine exactly why a particular code path <a name="iddle2122"></a><a name="iddle2123"></a><a name="iddle2124"></a><a name="iddle2125"></a><a name="iddle2126"></a>was taken.

<a name="ch08lev2sec13"></a>

#### 8.2.9\. gcc (GNU Compiler Collection)

<tt>gcc</tt> is the most <a name="iddle2127"></a><a name="iddle2128"></a>popular compiler used by Linux systems. Like all compilers, <tt>gcc</tt> <a name="iddle2129"></a><a name="iddle2130"></a><a name="iddle2131"></a>takes source code (such as C, C++, or Objective-C) and generates binaries. It provides many options to optimize the resultant binary, as well as options that make it easier to track the performance of an application. The details of <tt>gcc</tt>'s performance optimization options are not covered in this book, but you should investigate them when trying to increase an application's performance. <tt>gcc</tt> provides performance optimization options that enable you to tune the performance of compiled binaries using architecture generic optimizations (using <tt>-01, -02, -03</tt>), architecture-specific optimizations <tt>(-march</tt> and <tt>-mcpu</tt>), and feedback-directed optimization (using <tt>-fprofile-arcs</tt> and <tt>-fbranch-probabilities</tt>). More details on each of the optimization options are provided in the <tt>gcc</tt> man page.

<a name="ch08lev3sec17"></a>

##### 8.2.9.1 Performance-Related Options

<tt>gcc</tt> can be invoked in its most basic form as follows:

<pre>gcc [-g level] [-pg] -o prog_name source.c

</pre>

<tt>gcc</tt> has an enormous number of options that influence how it compiles an application. If you feel brave, take a look at them in the <tt>gcc</tt> man page. The particular options that can help during a performance investigation are shown <a name="iddle2132"></a><a name="iddle2133"></a><a name="iddle2134"></a><a name="iddle2135"></a><a name="iddle2136"></a>in [Table 8-5](ch08lev1sec2.html#ch08table05).

<a name="ch08table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 8-5\. <span class="docEmphasis"><tt>gcc</tt></span> Command-Line Options

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

<a name="iddle2137"></a><tt>-g[1 | 2 | 3]</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2138"></a>The <tt>-g</tt> option adds debugging information to the binary with a default level of 2\. If a level is specified, <tt>gcc</tt> adjusts the amount of debugging information stored in the binary. Level 1 provides only enough information to generate backtraces, but no information on the source-line mappings of particular lines of code. Level 3 provides more information than level 2, such as the macro definitions present in the source.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-pg</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle2139"></a>This turns on application profiling.

</td>

</tr>

</tbody>

</table>

Many performance investigation tools, such as <tt>oprofile</tt>, require an application to be compiled with debugging information to map performance information back to a particular line of application source code. They will generally still work without the debugging information, but if debugging is enabled, they will provide richer information. Application profiling was described in more detail in a <a name="iddle2140"></a><a name="iddle2141"></a><a name="iddle2142"></a><a name="iddle2143"></a><a name="iddle2144"></a>previous chapter.

<a name="ch08lev3sec18"></a>

##### 8.2.9.2 Example Usage

Probably the <a name="iddle2145"></a><a name="iddle2146"></a><a name="iddle2147"></a>best way to understand the type of debugging information that <tt>gcc</tt> can provide is to see a simple example. In [Listing 8.12](ch08lev1sec2.html#ch08ex12), we have the source for the C application, <tt>deep.c</tt>, which just calls a series of functions and then prints out the string <tt>"hi"</tt> a number of times depending on what number was passed in. The application's <tt>main</tt> function calls function <tt>a()</tt>, which calls function <tt>b()</tt> and then prints out <tt>"hi"</tt>.

<a name="ch08ex12"></a>

##### Listing 8.12\.

<pre>void b(int count)

{

  int i;

  for (i=0; i<count;i++)

    {printf("hi\n");}

}

void a(int count)

{

  b(count);

}

int main()

{

  a(10);

}

</pre>

First, as <a name="iddle2148"></a><a name="iddle2149"></a><a name="iddle2150"></a><a name="iddle2151"></a><a name="iddle2152"></a>shown in [Listing 8.13](ch08lev1sec2.html#ch08ex13), we compile the application without any debugging information. We then start the application in the debugger and add a breakpoint to the <tt>b()</tt> function. When we run the application, it stops at function <tt>b()</tt>, and we ask for a backtrace. <tt>gdb</tt> can figure out the backtrace, but it does not know what values were passed between functions or where the function exists in the original source file.

<a name="ch08ex13"></a>

##### Listing 8.13\.

<pre>[ezolt@wintermute utils]$ gcc -o deep deep.c

[ezolt@wintermute utils]$ gdb ./deep

...

(gdb) break b

Breakpoint 1 at 0x804834e

(gdb) run

Starting program: /usr/src/perf/utils/deep

(no debugging symbols found)...(no debugging symbols found)...

Breakpoint 1, 0x0804834e in b ()

<span class="docEmphStrong">(gdb) bt

#0  0x0804834e in b ()

#1  0x08048389 in a ()

#2  0x080483a8 in main ()</span>

</pre>

In [Listing 8.14](ch08lev1sec2.html#ch08ex14), we compile the same application with debugging information turned on. Now when we run gdb and generate a backtrace, we can see which values were passed to each function call and the exact line of source where a particular line of code <a name="iddle2153"></a><a name="iddle2154"></a><a name="iddle2155"></a><a name="iddle2156"></a><a name="iddle2157"></a>resides.

<a name="ch08ex14"></a>

##### Listing 8.14\.

<pre>[ezolt@wintermute utils]$ gcc -g -o deep deep.c

[ezolt@wintermute utils]$ gdb ./deep

..

(gdb) break b

Breakpoint 1 at 0x804834e: file deep.c, line 3.

(gdb) run

Starting program: /usr/src/perf/utils/deep

Breakpoint 1, b (count=10) at deep.c:3

3         for (i=0; i<count;i++)

<span class="docEmphStrong">(gdb) bt

#0  b (count=10) at deep.c:3

#1  0x08048389 in a (count=10) at deep.c:9

#2  0x080483a8 in main () at deep.c:14</span>

</pre>

Debugging information can significantly add to the size of the final executable that <tt>gcc</tt> generates. However, the information that it provides is invaluable when tracking a performance <a name="iddle2158"></a><a name="iddle2159"></a><a name="iddle2160"></a><a name="iddle2161"></a><a name="iddle2162"></a>problem.