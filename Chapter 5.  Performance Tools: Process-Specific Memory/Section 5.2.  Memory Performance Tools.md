### 5.2\. Memory Performance Tools

This section examines the various memory performance tools that enable you to investigate how a given application is using the memory subsystem, including the amount and different types of memory that a process is using, where it is being allocated, and how effectively the process is using the processor's cache.

<a name="ch05lev2sec1"></a>

#### 5.2.1\. ps

<tt>ps</tt> is an excellent <a name="iddle1130"></a><a name="iddle1131"></a><a name="iddle1132"></a><a name="iddle1133"></a>command to track a process's dynamic memory usage. In addition to the CPU statistics already mentioned, <tt>ps</tt> gives detailed information about the amount of memory that the application is using and how that memory usage affects the system.

<a name="ch05lev3sec1"></a>

##### 5.2.1.1 Memory Performance-Related Options

<tt>ps</tt> has many different options and can <a name="iddle1134"></a>retrieve many different statistics about the state of a running application. As you saw in the previous chapter, <tt>ps</tt> can retrieve information about the CPU that a process is spending, but it also can retrieve information about the amount and type of memory that a process is using. It can be invoked with the following command line:

<pre>ps [-o vsz,rss,tsiz,dsiz,majflt,minflt,pmem,command] <PID>

</pre>

[Table 5-1](ch05lev1sec2.html#ch05table01) describes the different types of memory statistics that <tt>ps</tt> can <a name="iddle1135"></a><a name="iddle1136"></a><a name="iddle1137"></a><a name="iddle1138"></a>display for a given PID.

<a name="ch05table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-1\. <span class="docEmphasis"><tt>ps</tt></span> Command-Line Options

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1139"></a><a name="iddle1140"></a><a name="iddle1141"></a><a name="iddle1142"></a>Option

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

<td class="docTableCell" align="left" valign="top">

<a name="iddle1143"></a><a name="iddle1144"></a>Enables you to specify exactly what process statistics you want to track. The different statistics are specified in a comma-separated list with no spaces.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>vsz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1145"></a>Statistic: The virtual set size is the amount of virtual memory that the application is using. Because Linux only allocated physical memory when an application tries to use it, this value may be much greater than the amount of physical memory the application is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rss</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1146"></a>Statistic: The resident set size is the amount of physical memory the application is currently using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1147"></a><a name="iddle1148"></a><a name="iddle1149"></a><a name="iddle1150"></a><tt>tsiz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1151"></a>Statistic: Text size is the virtual size of the program code. Once again, this isn't the physical size but rather the virtual size; however, it is a good indication of the size of the program.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>dsiz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1152"></a>Statistic: Data size is the virtual size of the program's data usage. This is a good indication of the size of the data structures and stack of the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>majflt</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1153"></a>Statistic: Major faults are the number of page faults that caused Linux to read a page from disk on behalf of the process. This may happen if the process accessed a piece of data or instruction that remained on the disk and Linux loaded it seamlessly for the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>minflt</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1154"></a>Statistic: Minor faults are the number of faults that Linux could fulfill without resorting to a disk read. This might happen if the application touches a piece of memory that has been allocated by the Linux kernel. In this case, it is not necessary to go to disk, because the kernel can just pick a free piece of memory and assign it to the application.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>pmep</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1155"></a>Statistic: The percentage of the system memory that the process is consuming.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>command</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1156"></a>Statistic: This is the command name.

</td>

</tr>

</tbody>

</table>

As mentioned in the preceding chapter, <tt>ps</tt> is flexible in regards to how you select the group of PIDs for which statistics display. <tt>ps —help</tt> provides information on how to specify different groups of <a name="iddle1157"></a>PIDs.

<a name="ch05lev3sec2"></a>

##### 5.2.1.2 Example Usage

[Listing 5.1](ch05lev1sec2.html#ch05ex01) shows the burn test <a name="iddle1158"></a>application running on the system. We ask <tt>ps</tt> to tell us information about the memory statistics of the process.

<a name="ch05ex01"></a>

##### Listing 5.1\.

<pre>[ezolt@wintermute tmp]$ ps –o vsz,rss,tsiz,dsiz,majflt,minflt,cmd 10882

  VSZ  RSS TSIZ DSIZ MAJFLT MINFLT CMD

11124 10004   1 11122    66   2465 ./burn

</pre>

<a name="iddle1159"></a><a name="iddle1160"></a><a name="iddle1161"></a>As [Listing 5.1](ch05lev1sec2.html#ch05ex01) shows, the burn application has a very small text size (1KB), but a very large data size (11,122KB). Of the total virtual size (11,124KB), the process has a slightly smaller resident set size (10,004KB), which represents the total amount of physical memory that the process is actually using. In addition, most of the faults generated by burn were minor faults, so most of the memory faults were due to memory allocation rather than loading in a large amount of text or data from the program image on the <a name="iddle1162"></a><a name="iddle1163"></a><a name="iddle1164"></a><a name="iddle1165"></a>disk.

<a name="ch05lev2sec2"></a>

#### 5.2.2\. /proc/<PID>

The Linux <a name="iddle1166"></a><a name="iddle1167"></a><a name="iddle1168"></a><a name="iddle1169"></a>kernel provides a virtual file system that enables you to extract information about the processes running on the system. The information provided by the <tt>/proc</tt> file system is usually only used by performance tools such as <tt>ps</tt> to extract performance data from the kernel. Although it is not normally necessary to dig through the files in <tt>/proc</tt>, it does provide some information that you cannot retrieve with other performance tools. In addition to many other statistics, <tt>/proc</tt> provides information about a process's use of memory and mapping of libraries.

<a name="ch05lev3sec3"></a>

##### 5.2.2.1 Memory Performance-Related Options

The interface <a name="iddle1170"></a><a name="iddle1171"></a><a name="iddle1172"></a><a name="iddle1173"></a>to <tt>/proc</tt> is straightforward. <tt>/proc</tt> provides many virtual files that you can <tt>cat</tt> to extract their information. Each running PID in the system has a subdirectory in <tt>/proc</tt>. Within this subdirectory is a series of files containing information about that PID. One of these files, status, provides information about the status of a given process PID. You can retrieve this information by using the following command:

<pre>cat /proc/<PID>/status

</pre>

[Table 5-2](ch05lev1sec2.html#ch05table02) describes <a name="iddle1174"></a><a name="iddle1175"></a><a name="iddle1176"></a><a name="iddle1177"></a>the memory statistics displayed in the status file.

<a name="ch05table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-2\. <span class="docEmphasis"><tt>/proc/<PID>/status</tt></span> Field Description

</caption><colgroup><col width="80"><col width="420"></colgroup>

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

<tt>VmSize</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the process's virtual set size, which is the amount of virtual memory that the application is using. Because Linux only allocates physical memory when an application tries to use it, this value may be much greater than the amount of physical memory the application is actually using. This is the same as the <tt>vsz</tt> parameter provided by <tt>ps</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmLck</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1178"></a>This is the amount of memory that has been locked by this process. Locked memory cannot be swapped to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmRSS</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1179"></a>This is the resident set size or amount of physical memory the application is currently using. This is the same as the <tt>rss</tt> statistic provided by <tt>ps</tt>.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmData</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1180"></a>This is the data size or the virtual size of the program's data usage. Unlike <tt>ps dsiz</tt> statistic, this does not include stack information.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmStk</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1181"></a>This is the size of the process's stack.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmExe</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1182"></a>This is the virtual size of the executable memory that the program has. It does not include libraries that the process is using.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>VmLib</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the size of the libraries that the process is using.

</td>

</tr>

</tbody>

</table>

<a name="iddle1183"></a><a name="iddle1184"></a><a name="iddle1185"></a><a name="iddle1186"></a>Another <a name="iddle1187"></a><a name="iddle1188"></a><a name="iddle1189"></a><a name="iddle1190"></a>one of the files present in the <tt><PID></tt> directory is the <tt>maps</tt> file. This provides information about how the process's virtual address space is used. You can retrieve it by using the following command:

<pre>cat /proc/<PID>/maps

</pre>

[Table 5-3](ch05lev1sec2.html#ch05table03) describes the fields shown in the <tt>maps</tt> file.

<a name="ch05table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-3\. <span class="docEmphasis"><tt>/proc/<PID>/maps</tt></span> Field Description

</caption><colgroup><col width="80"><col width="420"></colgroup>

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

<tt>Address</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This is the address range within the process where the library is mapped.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Permissions</tt>

</td>

<td class="docTableCell" align="left" valign="top">

These are the permissions of the memory region, where r = read, w = write, x = execute, s = shared, and p = private (copy on write).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Offset</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1191"></a>This is the offset into the library/application where the memory region mapping begins.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Device</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1192"></a>This is the device (minor and major number) where this particular file exists.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Inode</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1193"></a>This is the inode number of the mapped file.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Pathname</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1194"></a>This is the path name of the file that is mapped into the process.

</td>

</tr>

</tbody>

</table>

The information that <tt>/proc</tt> provides can help you understand how an application is allocating memory and which libraries it is <a name="iddle1195"></a><a name="iddle1196"></a><a name="iddle1197"></a><a name="iddle1198"></a>using.

<a name="ch05lev3sec4"></a>

##### 5.2.2.2 Example Usage

[Listing 5.2](ch05lev1sec2.html#ch05ex02) <a name="iddle1199"></a><a name="iddle1200"></a><a name="iddle1201"></a><a name="iddle1202"></a>shows the burn test application running on the system. First, we use <tt>ps</tt> to find the PID (4540) of burn. Then we extract the process's memory statistics using the <tt>/proc</tt> status file.

<a name="ch05ex02"></a>

##### Listing 5.2\.

<pre>[ezolt@wintermute tmp]$ ps aux | grep burn

ezolt     4540  0.4  2.6 11124 10004 pts/0   T    08:26   0:00 ./burn

ezolt     4563  0.0  0.1  1624  464 pts/0    S    08:29   0:00 grep burn

[ezolt@wintermute tmp]$ cat /proc/4540/status

Name:   burn

State:  T (stopped)

Tgid:   4540

Pid:    4540

PPid:   1514

TracerPid:      0

Uid:    501     501     501     501

Gid:    501     501     501     501

FDSize: 256

Groups: 501 9 502

VmSize:    11124 kB

VmLck:         0 kB

VmRSS:     10004 kB

VmData:     9776 kB

VmStk:         8 kB

VmExe:         4 kB

VmLib:      1312 kB

SigPnd: 0000000000000000

ShdPnd: 0000000000000000

SigBlk: 0000000000000000

SigIgn: 0000000000000000

SigCgt: 0000000000000000

CapInh: 0000000000000000

CapPrm: 0000000000000000

CapEff: 0000000000000000

</pre>

As [Listing 5.2](ch05lev1sec2.html#ch05ex02) shows, once again we see that the burn application has a very small text size (4KB) and stack size (8KB), but a very large data size (9,776KB) and a reasonably sized library size (1,312KB). The small text size means that the process does not have much executable code, whereas the moderate library size means that it is using a library to support its execution. The small stack size means that the process is not calling deeply nested functions or is not calling functions that use large or many temporary variables. The <tt>VmLck</tt> size of 0KB means that the process has not locked any pages into memory, making them unswappable. The <tt>VmRSS</tt> size of 10,004KB means that the application is currently using 10,004KB of physical memory, although it has either allocated or mapped the <tt>VmSize</tt> or 11,124KB. If the application begins to use the memory that it has allocated but is not currently using, the <tt>VmRSS</tt> size increases but leaves the <tt>VmSize</tt> unchanged.

As noted previously, the application's <tt>VmLib</tt> size is nonzero, so it is using a library. In [Listing 5.3](ch05lev1sec2.html#ch05ex03), we look at the process's maps to see the exact libraries it <a name="iddle1207"></a><a name="iddle1208"></a><a name="iddle1209"></a><a name="iddle1210"></a>is using.

<a name="ch05ex03"></a>

##### Listing 5.3\.

<pre>[ezolt@wintermute test_app]$ cat /proc/4540/maps

08048000-08049000 r-xp 00000000 21:03 393730      /tmp/burn

08049000-0804a000 rw-p 00000000 21:03 393730      /tmp/burn

0804a000-089d3000 rwxp 00000000 00:00 0

40000000-40015000 r-xp 00000000 21:03 1147263     /lib/ld-2.3.2.so

40015000-40016000 rw-p 00015000 21:03 1147263     /lib/ld-2.3.2.so

4002e000-4002f000 rw-p 00000000 00:00 0

4002f000-40162000 r-xp 00000000 21:03 2031811     /lib/tls/libc-2.3.2.so

40162000-40166000 rw-p 00132000 21:03 2031811     /lib/tls/libc-2.3.2.so

40166000-40168000 rw-p 00000000 00:00 0

bfffe000-c0000000 rwxp fffff000 00:00 0

</pre>

As you see in [Listing 5.3](ch05lev1sec2.html#ch05ex03), the burn application is using two libraries: <tt>ld</tt> and <tt>libc</tt>. The text section (denoted by the permission <tt>r-xp</tt>) of <tt>libc</tt> has a range of 0x4002f000 through 0x40162000 or a size of 0x133000 or 1,257,472 bytes.

The data section (denoted by permission <tt>rw-p</tt>) of <tt>libc</tt> has a range of 40162000 through 40166000 or a size of 0x4000 or 16,384 bytes. The text size of <tt>libc</tt> is bigger than <tt>ld</tt>'s text size of 0x15000 or 86,016 bytes. The data size of <tt>libc</tt> is also bigger than <tt>ld</tt>'s text size of 0x1000 or 4,096 bytes. <tt>libc</tt> is the big library <a name="iddle1211"></a><a name="iddle1212"></a><a name="iddle1213"></a><a name="iddle1214"></a>that burn is linking in.

<tt>/proc</tt> proves to be a useful way to extract performance statistics directly from the kernel. Because the statistics are text based, you can use the standard Linux tools to access them.

<a name="ch05lev2sec3"></a>

#### 5.2.3\. memprof

<tt>memprof</tt> is a <a name="iddle1215"></a><a name="iddle1216"></a><a name="iddle1217"></a><a name="iddle1218"></a>graphical memory-usage profiling tool. It shows how a program is allocating memory as it runs. <tt>memprof</tt> shows the amount of memory your application is consuming and which functions are responsible for the memory consumption. In addition, <tt>memprof</tt> can show which code paths are responsible for memory usage. For example, if a function <tt>foo()</tt> allocates no memory, but calls a function <tt>bar()</tt>, which allocates a large amount of memory, <tt>memprof</tt> shows you how much <tt>foo()</tt> itself used and all the functions that <tt>foo()</tt> called. <tt>memprof</tt> updates this information dynamically as the application is running.

<a name="ch05lev3sec5"></a>

##### 5.2.3.1 Memory Performance-Related Options

<tt>memprof</tt> is a graphical application, but has a few command-line options that modify its execution. It is invoked with the following command:

<pre>memprof [--follow-fork] [--follow-exec] application

</pre>

<tt>memprof</tt> profiles the given "application" and creates a graphical display of its memory usage. Although <tt>memprof</tt> can be run on any application, it can provide more information if the application and the libraries that it relies on are compiled with debugging symbols.

[Table 5-4](ch05lev1sec2.html#ch05table04) describes the options that manipulate the behavior of <tt>memprof</tt> if it is monitoring an application that calls <tt>fork</tt> or <tt>exec</tt>. This normally happens when an application launches a new process or executes a new <a name="iddle1219"></a><a name="iddle1220"></a><a name="iddle1221"></a><a name="iddle1222"></a>command.

<a name="ch05table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-4\. <span class="docEmphasis"><tt>memprof</tt></span> Command-Line Options

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

<tt>--follow-fork</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1223"></a>This option will cause <tt>memprof</tt> to launch a new window for the newly forked process.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--follow-exec</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1224"></a>This option will cause <tt>memprof</tt> to continue profiling an application after it has called exec.

</td>

</tr>

</tbody>

</table>

Once invoked, <tt>memprof</tt> creates a window with a series of menus and options that enable you to select an application that you are going to <a name="iddle1225"></a><a name="iddle1226"></a><a name="iddle1227"></a><a name="iddle1228"></a>profile.

<a name="ch05lev3sec6"></a>

##### 5.2.3.2 Example Usage

Suppose that I have <a name="iddle1229"></a><a name="iddle1230"></a><a name="iddle1231"></a>the example code in [Listing 5.4](ch05lev1sec2.html#ch05ex04) and I want to profile it. In this application, which I call <tt>memory_eater</tt>, the function <tt>foo()</tt> does not allocate any memory, but it calls the function <tt>bar()</tt>, which does.

<a name="ch05ex04"></a>

##### Listing 5.4\.

<pre>#include <stdlib.h>

void bar(void)

{

  malloc(10000);

}

void foo(void)

{

  int i;

  for (i=0; i<100;i++)

    bar();

}

int main()

{

  foo();

  while(1);

}

</pre>

After compiling this application with the <tt>-g3</tt> flag (so that the application has symbols included), we use <tt>memprof</tt> to profile this <a name="iddle1232"></a><a name="iddle1233"></a><a name="iddle1234"></a>application:

<pre>[ezolt@localhost example]$ memprof ./memory_eater memintercept (3965):

_MEMPROF_SOCKET = /tmp/memprof.Bm1AKu memintercept (3965): New process,

operation = NEW, old_pid = 0

</pre>

<tt>memprof</tt> creates the application window shown in [Figure 5-1](ch05lev1sec2.html#ch05fig01). As you can see, it shows memory usage information about the <tt>memory_eater</tt> application, as well as a series of buttons and menus that enable you to manipulate the <a name="iddle1235"></a><a name="iddle1236"></a><a name="iddle1237"></a><a name="iddle1238"></a><a name="iddle1239"></a><a name="iddle1240"></a>profile.

<a name="ch05fig01"></a>

<center>

##### Figure 5-1\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig01_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig01_alt.jpg)

[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig01_alt.jpg)<a name="iddle1241"></a><a name="iddle1242"></a><a name="iddle1243"></a><a name="iddle1244"></a><a name="iddle1245"></a><a name="iddle1246"></a>If you click the Profile button, <tt>memprof</tt> shows the memory profile of the application. The first information box in [Figure 5-2](ch05lev1sec2.html#ch05fig02) shows how much memory each function is consuming (denoted by "self"), as well as the sum of the memory that the function and its children are consuming (denoted by "total"). As expected, the <tt>foo()</tt> function does not allocate any memory, so its self value is 0, whereas its total value is 100,000, because it is calling a function that does allocate memory.

<a name="ch05fig02"></a>

<center>

##### Figure 5-2\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig02_alt.jpg)</div>

</center>

[  

The children and callers information boxes change as you click different functions in the top box. This way, you can see which functions of an application are using memory.

](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig02_alt.jpg)

[<tt>memprof</tt> provides a way to graphically traverse through a large amount of data about memory allocation. It provides an easy way to determine the memory allocation of a given function and each functions that it](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig02_alt.jpg) <a name="iddle1247"></a><a name="iddle1248"></a><a name="iddle1249"></a><a name="iddle1250"></a><a name="iddle1251"></a><a name="iddle1252"></a>calls.<a name="iddle1253"></a><a name="iddle1254"></a><a name="iddle1255"></a><a name="iddle1256"></a><a name="iddle1257"></a><a name="iddle1258"></a>

<a name="ch05lev2sec4"></a>

#### 5.2.4\. valgrind (cachegrind)

<tt>valgrind</tt> is a <a name="iddle1259"></a><a name="iddle1260"></a><a name="iddle1261"></a><a name="iddle1262"></a>powerful tool that enables you to debug tricky memory-management errors. Although <tt>valgrind</tt> is mainly a developer's tool, it also has a "skin" that can show processor cache usage. <tt>valgrind</tt> simulates the current processor and runs the application in this virtual processor while tracking memory usage. It can also simulate the processor cache and pinpoint where a program is hitting and missing in the instruction and data caches.

Although very useful, its cache statistics are inexact (because <tt>valgrind</tt> is only a simulation of the processor rather than an actual piece of hardware). <tt>valgrind</tt> will not account for cache misses normally caused by system calls to the Linux kernel or cache misses that happen because of context switching. In addition, <tt>valgrind</tt> runs applications at a much slower speed than a natively executing program. However, <tt>valgrind</tt> provides a great first approximation of the cache usage of an application. <tt>valgrind</tt> can be run on any executable; if the program has been compiled with symbols (passed as <tt>-g3</tt> to <tt>gcc</tt> when compiling), however, it will be able to pinpoint the exact line of code responsible for the cache <a name="iddle1263"></a><a name="iddle1264"></a><a name="iddle1265"></a><a name="iddle1266"></a>usage.

<a name="ch05lev3sec7"></a>

##### 5.2.4.1 Memory Performance-Related Options

When using <tt>valgrind</tt> to analyze cache usage for a particular application, there are two phases: collection and annotation. The collection phase starts with the following command line:

<pre>valgrind --skin=cachegrind application

</pre>

<tt>valgrind</tt> is a flexible tool that has a few different "skins" that allow it to perform different types of analysis. During the collection phase, <tt>valgrind</tt> uses the <tt>cachegrind</tt> skin to collect information about cache usage. The <tt>application</tt> in the preceding command line represents the application to profile. The collection phase prints summary information to the screen, but it also saves more detailed statistics in a file named <tt>cachegrind.out.pid</tt>, where <tt>pid</tt> is the PID of the profiled application as it was running. When the collection phase is complete, the command <tt>cg_annoate</tt> is used to map the cache usage back to the application source code. <tt>cg_annote</tt> is invoked in the following way:

<pre>cg_annotate --pid [--auto=yes|no]

</pre>

<tt>cg_annotate</tt> takes the information generated by <tt>valgrind</tt> and uses it to annotate the application that was profiled. The <tt>--pid</tt> option is required, where <tt>pid</tt> is the PID of the profile that you are interested in. By default, <tt>cg_annotate</tt> just shows cache usage at the function level. If you set <tt>--auto=yes</tt>, cache usage displays at <a name="iddle1267"></a><a name="iddle1268"></a><a name="iddle1269"></a><a name="iddle1270"></a>the source-line level.

<a name="ch05lev3sec8"></a>

##### 5.2.4.2 Example Usage

This example <a name="iddle1271"></a>shows <tt>valgrind</tt> (v2.0) running on a simple application. The application clears a large area of memory and then calls two functions, <tt>a()</tt> and <tt>b()</tt>, and each touches this memory. Function <tt>a()</tt> touches the memory ten times as often as function <tt>b()</tt>.

First, as shown in [Listing 5.5](ch05lev1sec2.html#ch05ex05), we run <tt>valgrind</tt> on the application using the <tt>cachegrind</tt> <a name="iddle1272"></a><a name="iddle1273"></a><a name="iddle1274"></a><a name="iddle1275"></a>skin.

<a name="ch05ex05"></a>

##### Listing 5.5\.

<pre>[ezolt@wintermute test_app]$  valgrind --skin=cachegrind ./burn

==25571== Cachegrind, an I1/D1/L2 cache profiler for x86-linux.

==25571== Copyright (C) 2002-2003, and GNU GPL'd, by Nicholas Nethercote.

==25571== Using valgrind-2.0.0, a program supervision framework for x86-linux.

==25571== Copyright (C) 2000-2003, and GNU GPL'd, by Julian Seward.

==25571== Estimated CPU clock rate is 468 MHz

==25571== For more details, rerun with: -v

==25571==

==25571==

==25571== I   refs:      11,317,111

==25571== I1  misses:           215

==25571== L2i misses:           214

==25571== I1  miss rate:        0.0%

==25571== L2i miss rate:        0.0%

==25571==

==25571== D   refs:       6,908,012 (4,405,958 rd + 2,502,054  wr)

==25571== D1  misses:     1,412,821  (1,100,287 rd +    312,534 wr)

==25571== L2d misses:       313,810  (    1,276 rd +    312,534 wr)

==25571== D1  miss rate:       20.4% (     24.9%   +       12.4%  )

==25571== L2d miss rate:        4.5% (      0.0%   +       12.4%  )

==25571==

==25571== L2 refs:        1,413,036  (1,100,502 rd +    312,534 wr)

==25571== L2 misses:        314,024  (    1,490 rd +    312,534 wr)

==25571== L2 miss rate:         1.7% (      0.0%   +       12.4%  )

</pre>

In the <a name="iddle1276"></a><a name="iddle1277"></a><a name="iddle1278"></a><a name="iddle1279"></a>run of [Listing 5.5](ch05lev1sec2.html#ch05ex05), the application executed 11,317,111 instructions; this is shown by the <tt>I refs</tt> statistics. The process had an astonishingly low number of misses in both the L1 (215) and L2 (216) instruction cache, as denoted by an <tt>I1</tt> and <tt>L2i</tt> miss rate of 0.0 percent. The process had a total number of 6,908,012 data references, 4,405,958 were reads and 2,502,054 were writes. 24.9 percent of the reads and 12.4 percent of the writes could not be satisfied by the L1 cache. Luckily, we can almost always satisfy the reads in the L2 data, and they are shown to have a miss rate of 0 percent. The writes are still a problem with a miss rate of 12.4 percent. In this application, memory access of the data is the problem to investigate.

The ideal application would have a very low number of instruction cache and data cache misses. To eliminate instruction cache misses, it may be possible to recompile the application with different compiler options or trim code, so that the hot code does not have to share <tt>icache</tt> space with the code that is not used often. To eliminate data cache misses, use arrays for data structures rather than linked lists, if possible, and reduce the size of elements in data structures, and access memory in a cache-friendly way. In any event, <tt>valgrind</tt> helps to point out which accesses/data structures should be optimized. This application run summary shows that data accesses are the main problem.

As shown in [Listing 5.5](ch05lev1sec2.html#ch05ex05), this command displays cache usage statistics for the overall run. However, when developing an application, or investigating a performance problem, it is often more interesting to see where cache misses happen rather than just the totals during an application's runtime. To determine which functions are responsible for the cache misses, we run <tt>cg_annotate</tt>, as shown in [Listing 5.6](ch05lev1sec2.html#ch05ex06). This shows us which functions are responsible for which cache misses. As we expect, the function <tt>a()</tt> has 10 times (1,000,000) the misses of the <a name="iddle1280"></a><a name="iddle1281"></a><a name="iddle1282"></a><a name="iddle1283"></a>function <tt>b()</tt> (100,000).

<a name="ch05ex06"></a>

##### Listing 5.6\.

<pre>[ezolt@wintermute test_app]$ cg_annotate --25571

----------------------------------------------------------------------------------------

I1 cache:         16384 B, 32 B, 4-way associative

D1 cache:         16384 B, 32 B, 4-way associative

L2 cache:        131072 B, 32 B, 4-way associative

Command:         ./burn

Events recorded: Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Events shown:    Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Event sort order:Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Thresholds:      99 0 0 0 0 0 0 0 0

Include dirs:

User annotated:

Auto-annotation: off

----------------------------------------------------------------------------------------

        Ir I1mr I2mr        Dr      D1mr  D2mr        Dw    D1mw    D2mw

----------------------------------------------------------------------------------------

11,317,111  215  214 4,405,958 1,100,287 1,276 2,502,054 312,534 312,534  PROGRAM TOTALS

----------------------------------------------------------------------------------------

       Ir I1mr I2mr        Dr      D1mr D2mr        Dw    D1mw    D2mw  file:function

----------------------------------------------------------------------------------------

8,009,011    2    2 4,003,003 1,000,000  989     1,004       0        0  burn.c:a

2,500,019    3    3         6         1    1 2,500,001 312,500 312,500   ???:__GI_memset

  800,911    2    2   400,303   100,000    0       104       0        0  burn.c:b

</pre>

Although <a name="iddle1284"></a><a name="iddle1285"></a><a name="iddle1286"></a><a name="iddle1287"></a>a per-function breakdown of cache misses is useful, it would be interesting to see which lines within the application are actually causing the cache misses. If we use the <tt>--auto</tt> option, as demonstrated in [Listing 5.7](ch05lev1sec2.html#ch05ex07), <tt>cg_annotate</tt> tells us exactly which line is responsible for each miss.

<a name="ch05ex07"></a>

##### Listing 5.7\.

<pre>[ezolt@wintermute test_app]$ cg_annotate --25571 --auto=yes

----------------------------------------------------------------------------------------

I1 cache:         16384 B, 32 B, 4-way associative

D1 cache:         16384 B, 32 B, 4-way associative

L2 cache:         131072 B, 32 B, 4-way associative

Command:          ./burn

Events recorded:  Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Events shown:     Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Event sort order: Ir I1mr I2mr Dr D1mr D2mr Dw D1mw D2mw

Thresholds:       99 0 0 0 0 0 0 0 0

Include dirs:

User annotated:

Auto-annotation:  on

----------------------------------------------------------------------------------------

        Ir I1mr I2mr        Dr      D1mr  D2mr        Dw    D1mw    D2mw

----------------------------------------------------------------------------------------

11,317,111  215  214 4,405,958 1,100,287 1,276 2,502,054 312,534 312,534  PROGRAM TOTALS

----------------------------------------------------------------------------------------

       Ir I1mr I2mr        Dr      D1mr D2mr        Dw    D1mw    D2mw  file:function

----------------------------------------------------------------------------------------

8,009,011    2    2 4,003,003 1,000,000  989     1,004       0       0  burn.c:a

2,500,019    3    3         6         1    1 2,500,001 312,500 312,500  ???:__GI_memset

  800,911    2    2   400,303   100,000    0       104       0       0  burn.c:b

----------------------------------------------------------------------------------------

-- Auto-annotated source: burn.c

----------------------------------------------------------------------------------------

       Ir I1mr I2mr        Dr      D1mr D2mr    Dw D1mw D2mw

-- line 2 ----------------------------------------

        .    .    .         .         .    .     .    .    .

        .    .    .         .         .    .     .    .    .  #define ITER 100

        .    .    .         .         .    .     .    .    .  #define SZ 10000000

        .    .    .         .         .    .     .    .    .  #define STRI 10000

        .    .    .         .         .    .     .    .    .

        .    .    .         .         .    .     .    .    .  char test[SZ];

        .    .    .         .         .    .     .    .    .

        .    .    .         .         .    .     .    .    .  void a(void)

        3    0    0         .         .    .     1    0    0  {

        2    0    0         .         .    .     2    0    0    int i=0,j=0;

    5,004    1    1     2,001	      0    0     1    0    0    for(j=0;j<10*ITER ; j++)

5,004,000    0    0 2,001,000         0    0 1,000    0    0      for(i=0;i<SZ;i=i+STRI)

        .    .    .         .         .    .     .    .    .        {

3,000,000    1    1 2,000,000 1,000,000  989     .    .    .    test[i]++;

        .    .    .         .         .    .     .    .    .        }

        2    0    0         2         0    0     .    .     .   }

        .    .    .         .         .    .     .    .     .

        .    .    .         .         .    .     .    .     .   void b(void)

        3    1    1         .         .    .     1    0     0   {

        2    0    0         .         .    .     2    0     0     int i=0,j=0;

      504    0    0       201         0    0     1    0     0     for (j=0;j<ITER; j++)

  500,400    1    1   200,100         0    0   100    0     0       for (i=0;i<SZ;i=i+STRI)

        .    .    .         .         .    .     .    .     .         {

  300,000    0    0   200,000   100,000    0     .    .   .       test[i]++;

        .    .    .         .         .    .     .    .     .         }

        2    0    0         2         0    0     .    .     .   }

        .    .    .         .         .    .     .    .     .

        .    .    .         .         .    .     .    .     .

        .    .    .         .         .    .     .    .     .   main()

        6    2    2         .         .    .     1    0     0   {

        .    .    .         .         .    .     .    .     .

        .    .    .         .         .    .     .    .     .     /* Arbitrary value*/

        6    0    0         .         .    .     4    0     0     memset(test, 42, SZ);

        1    0    0         .         .    .     1    0     0     a();

        1    0    0         .         .    .     1    0     0     b();

        2    0    0         2         1    1     .    .     .   }

-----------------------------------------------------------------------------------------

Ir I1mr I2mr  Dr D1mr D2mr Dw D1mw D2mw

-----------------------------------------------------------------------------------------

78    3    3 100  100   78  0    0    0  percentage of events annotated

</pre>

As [Listing 5.7](ch05lev1sec2.html#ch05ex07) shows, we have a line-by-line breakdown of where different cache misses and hits are occurring. We can see that the inner <tt>for</tt> loops have almost all the data references. As we expect, the <tt>for</tt> loop in the <tt>a()</tt> function <a name="iddle1288"></a><a name="iddle1289"></a><a name="iddle1290"></a><a name="iddle1291"></a>has ten times those of the <tt>b()</tt> function.

The different level of detail (program level, function level, and line level) that <tt>valgrind</tt>/<tt>cachegrind</tt> provides can give you a good idea of which parts of an application are accessing memory and effectively using the processor caches.

<a name="ch05lev2sec5"></a>

#### 5.2.5\. kcachegrind

<tt>kcachegrind</tt> works <a name="iddle1292"></a><a name="iddle1293"></a><a name="iddle1294"></a><a name="iddle1295"></a>intimately with <tt>valgrind</tt> to provide detailed information about the cache usage of a profiled application. It adds two new pieces of functionality above that of standard <tt>valgrind</tt>. First, it provides a skin for <tt>valgrind</tt>, called <tt>calltree</tt>, that captures both cache and call-tree statistics for a particular application. Second, it provides a graphical exploration the cache performance information and innovative visuals of the data.

<a name="ch05lev3sec9"></a>

##### 5.2.5.1 Memory Performance-Related Options

Similar to <tt>valgrind</tt>, when using <tt>kcachegrind</tt> to analyze cache usage for a particular application, there are two phases: collection and annotation. The collection phase starts with the following command line:

<pre>calltree application

</pre>

The <tt>calltree</tt> command accepts many different options to manipulate the information to be collected. [Table 5-5](ch05lev1sec2.html#ch05table05) shows some of the more important <a name="iddle1296"></a><a name="iddle1297"></a><a name="iddle1298"></a><a name="iddle1299"></a>options.

<a name="ch05table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-5\. <span class="docEmphasis"><tt>calltree</tt></span> Command-Line Options

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

<tt>--help</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1300"></a>This provides a brief explanation of all the different collection methods that <tt>calltree</tt> supports.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-dump-instr=yes|no</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1301"></a>This is the amount of memory that has been locked by this process. Locked memory cannot be swapped to disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--trace-jump=yes|no</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This includes branching information, or information about which path is taken at each branch.

</td>

</tr>

</tbody>

</table>

<tt>calltree</tt> can record many different statistics. Refer to <tt>calltree</tt>'s <tt>help</tt> option for more details.

During the collection phase, <tt>valgrind</tt> uses the <tt>calltree</tt> skin to collect information about cache usage. The <tt>application</tt> in the preceding command line represents the application to profile. During the collection phase, <tt>calltree</tt> prints summary information to the screen and, identically to <tt>cachegrind</tt>, it also saves more detailed statistics in a file named <tt>cachegrind.out.pid</tt>, where <tt>pid</tt> is the PID of the profiled application as it was running.

When the collection phase is complete, the command <tt>kcachegrind</tt> is used to map the cache usage back to the application source <a name="iddle1302"></a><a name="iddle1303"></a><a name="iddle1304"></a><a name="iddle1305"></a>code. <tt>kcachegrind</tt> is invoked in the following way:

<pre>kcachegrind cachegrind.out.pid

</pre>

<tt>kcachegrind</tt> displays the cache profiles statistics that have been collected and enables you to navigate through the results.

<a name="ch05lev3sec10"></a>

##### 5.2.5.2 Example Usage

The first step <a name="iddle1306"></a><a name="iddle1307"></a><a name="iddle1308"></a><a name="iddle1309"></a>in using <tt>kcachegrind</tt> is to compile the application with symbols to allow sample-to-source line mappings. This is done with the following command:

<pre>[ezolt@wintermute test_app]$ gcc -o burn burn.c -g3

</pre>

Next, run <tt>calltree</tt> against that application, as shown in [Listing 5.8](ch05lev1sec2.html#ch05ex08). This provides output similar to <tt>cachegrind</tt>, but, most importantly, it generates a <tt>cachegrind.out</tt> file, which will be used by <a name="iddle1310"></a><a name="iddle1311"></a><a name="iddle1312"></a><a name="iddle1313"></a><tt>kcachegrind</tt>.

<a name="ch05ex08"></a>

##### Listing 5.8\.

<pre>[ezolt@wintermute test_app]$ calltree --dump-instr=yes --trace-jump=yes ./burn

==12242== Calltree-0.9.7, a call-graph generating cache profiler for x86-linux.

==12242== Copyright (C) 2002-2004, and GNU GPL'd, by N.Nethercote and J.Weidendorfer.

==12242== Using valgrind-2.0.0, a program supervision framework for x86-linux.

==12242== Copyright (C) 2000-2003, and GNU GPL'd, by Julian Seward.

==12242== Estimated CPU clock rate is 469 MHz

==12242== For more details, rerun with: -v

==12242==

==12242==

==12242== I   refs:       33,808,151

==12242== I1  misses:            216

==12242== L2i misses:            215

==12242== I1  miss rate:         0.0%

==12242== L2i miss rate:         0.0%

==12242==

==12242== D   refs:       29,404,027  (4,402,969 rd + 25,001,058 wr)

==12242== D1  misses:      4,225,324  (1,100,290 rd +  3,125,034 wr)

==12242== L2d misses:      4,225,324  (1,100,290 rd +  3,125,034 wr)

==12242== D1  miss rate:        14.3% (     24.9%   +       12.4% )

==12242== L2d miss rate:        14.3% (     24.9%   +       12.4% )

==12242==

==12242== L2 refs:         4,225,540  (1,100,506 rd +  3,125,034 wr)

==12242== L2 misses:       4,225,539  (1,100,505 rd +  3,125,034 wr)

==12242== L2 miss rate:          6.6%  (     2.8%   +       12.4% )

</pre>

When we have the <tt>cachegrind.out</tt> file, we can start <tt>kcachegrind</tt> (v.0.54) to analyze the data by using the following <a name="iddle1314"></a><a name="iddle1315"></a><a name="iddle1316"></a><a name="iddle1317"></a>command:

<pre>[ezolt@wintermute test_app]$ kcachegrind cachegrind.out.12242

</pre>

This brings up the window shown in [Figure 5-3](ch05lev1sec2.html#ch05fig03). The window shows a flat profile of all the cache misses in the left pane. By default, data read misses from the L1 cache are shown.

<a name="ch05fig03"></a>

<center>

##### Figure 5-3\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig03_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig03_alt.jpg)

[Next, in](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig03_alt.jpg) [Figure 5-4](ch05lev1sec2.html#ch05fig04), in the upper-right pane, we can see a visualization of the callee map, or all the functions (<tt>a()</tt> and <tt>b()</tt>) that the function in the left pane (<tt>main</tt>) calls. In the lower-right pane, we can see the application's call graph.<a name="iddle1318"></a><a name="iddle1319"></a><a name="iddle1320"></a><a name="iddle1321"></a>

<a name="ch05fig04"></a>

<center>

##### Figure 5-4\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig04_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig04_alt.jpg)

[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig04_alt.jpg)<a name="iddle1322"></a><a name="iddle1323"></a><a name="iddle1324"></a><a name="iddle1325"></a>Finally, in [Figure 5-5](ch05lev1sec2.html#ch05fig05), we select a different function to examine in the left pane. We also select a different event to examine (instruction fetches) using the upper-right pane. Finally, we can visualize the loops in the assembly code using the lower-right pane.

<a name="ch05fig05"></a>

<center>

##### Figure 5-5\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig05_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig05_alt.jpg)

[These examples barely scratch the surface of what <tt>kcachegrind</tt> can do, and the best way to learn about it is to try it. <tt>kcachegrind</tt> is an extraordinarily useful tool for those who like to investigate performance issues](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/05fig05_alt.jpg) <a name="iddle1326"></a><a name="iddle1327"></a><a name="iddle1328"></a><a name="iddle1329"></a>visually.<a name="iddle1330"></a><a name="iddle1331"></a><a name="iddle1332"></a><a name="iddle1333"></a>

<a name="ch05lev2sec6"></a>

#### 5.2.6\. oprofile (III)

As you have <a name="iddle1334"></a><a name="iddle1335"></a><a name="iddle1336"></a><a name="iddle1337"></a>seen in previous chapters, <tt>oprofile</tt> is a powerful tool that can help to determine where application time is spent. However, <tt>oprofile</tt> can also work with the processor's performance counters to provide an accurate view of how it performs. Whereas <tt>cachegrind</tt> simulates the CPU to find cache misses/hits, <tt>oprofile</tt> uses the actual CPU performance counters to pinpoint the location of cache misses. Unlike <tt>cachegrind</tt>, <tt>oprofile</tt> does not simulate the processor, so cache effects that it records are real; those caused by the operating system will be visible. In addition, an application analyzed under <tt>oprofile</tt> will run at near native speeds, whereas <tt>cachegrind</tt> takes much longer. However, <tt>cachegrind</tt> is easier to set up and use than <tt>oprofile</tt>, and it can always track the same events no matter what version of x86 processor it runs on. <tt>cachegrind</tt> is a good tool to use when you need a quick and pretty accurate answer, whereas <tt>oprofile</tt> proves useful when you need more accurate statistics or need statistics that <tt>cachegrind</tt> does not provide.

<a name="ch05lev3sec11"></a>

##### 5.2.6.1 Memory Performance-Related Options

This discussion of <tt>oprofile</tt> does not add any new command-line options because they have already been described in section outlining CPU performance. However, one command becomes more important as you start to sample events different from <tt>oprofile</tt>'s defaults. Different processors and architectures can sample different sets of events and <tt>oprofile</tt>'s <tt>op_help</tt> command displays the list of events that your current processor <a name="iddle1338"></a><a name="iddle1339"></a><a name="iddle1340"></a><a name="iddle1341"></a>supports.

<a name="ch05lev3sec12"></a>

##### 5.2.6.2 Example Usage

As mentioned previously, the events that <tt>oprofile</tt> can monitor are processor specific, so these examples are run on my current machine, which is a Pentium-III. On the Pentium-III, we can use performance counters exposed by <tt>oprofile</tt> to gather the similar information that was provided by <tt>valgrind</tt> with the <tt>cachegrind</tt> skin. This uses the performance counter hardware rather than software simulation. Using the performance hardware presents two pitfalls. First, we must deal with the underlying hardware limitations of the performance counters. On the Pentium-III, <tt>oprofile</tt> can only measure two events simultaneously, whereas <tt>cachegrind</tt> could measure many types of memory events simultaneously. This means that for <tt>oprofile</tt> to measure the same events as <tt>cachegrind</tt>, we must run the application multiple times and change the events that <tt>oprofile</tt> monitors during each run. The second pitfall is the fact that <tt>oprofile</tt> does not provide an exact count of the events like <tt>cachegrind</tt>, only samples the counters, so we will be able to see where the events most likely occur, but we will not be able to see the exact number. In fact, we will only receive (1/sample rate) number of samples. If an application only causes an event to happen a few times, it might not be recorded at all. Although it can be frustrating to not know the exact number of events when debugging a performance problem, it is usually most important to figure the relative number of samples between code lines. Even though you will not be able to directly determine the total number of events that occurred at a particular source line, you will be able to figure out the line with most events, and that is usually enough to start debugging a performance problem. This inability to retrieve exact event counts is present in every form of CPU sampling and will be present on any processor performance hardware that implements it. However, it is really this limitation that allows this performance hardware to exist at all; without it, the performance monitoring would cause too much overhead.

<tt>oprofile</tt> can monitor many different types of events, which vary on different processors. This section outlines some of the important events on the Pentium-III for an example. The Pentium-III can monitor the L1 data cache (called the DCU on the Pentium-III) by using the following events (events and descriptions <a name="iddle1342"></a><a name="iddle1343"></a><a name="iddle1344"></a><a name="iddle1345"></a>provided by <tt>op_help</tt>):

<pre>[ezolt@localhost book]$ op_help

oprofile: available events for CPU type "PIII"

See Intel Architecture Developer's Manual Volume 3, Appendix A and Intel

Architecture Optimization Reference Manual (730795-001)

....

DCU_LINES_IN:     total lines allocated in the DCU

DCU_M_LINES_IN:   number of M state lines allocated in DCU

DCU_M_LINES_OUT:  number of M lines evicted from the DCU

DCU_MISS_OUTSTANDING: number of cycles while DCU miss outstanding

...

</pre>

Notice that we do not have an exact correspondence to what cachegrind provided, which was the number of "reads and writes" to the L1 data cache. However, we can figure out how many cycles of L1 data misses each function had by using the <tt>DCU_LINES_IN</tt> event. Although this event does not tell us the exact number of misses that each had, it should tell us how much each function missed in the cache relative to each other. The events monitoring the L2 data cache are a little closer, but it still does not have an exact correspondence to what cachegrind was providing. Here are the relevant L2 data cache events for the <a name="iddle1346"></a><a name="iddle1347"></a><a name="iddle1348"></a><a name="iddle1349"></a>Pentium-III:

<pre>[ezolt@localhost book]$ op_help

.....

L2_LD: number of L2 data loads

        Unit masks

        ----------

        0x08: (M)odified cache state

        0x04: (E)xclusive cache state

        0x02: (S)hared cache state

        0x01: (I)nvalid cache state

        0x0f: All cache states

L2_ST:  number of L2 data stores

        Unit masks

        ----------

        0x08: (M)odified cache state

        0x04: (E)xclusive cache state

        0x02: (S)hared cache state

        0x01: (I)nvalid cache state

        0x0f: All cache states

L2_LINES_IN: number of allocated lines in L2

....

</pre>

The <a name="iddle1350"></a><a name="iddle1351"></a><a name="iddle1352"></a><a name="iddle1353"></a>Pentium-III actually supports many more than these, but these are the basic load and store events. (<tt>cachegrind</tt> calls a load a "read" and a store a "write.") We can use these events to count the number of loads and stores that happened at each source line. We can also use the <tt>L2_LINES_IN</tt> to show which pieces of code had more L2 cache misses. As mentioned earlier, we will not get an exact value. In addition, on the Pentium-III, both instruction and data share the L2 cache. Any L2 misses could be the result of instruction or data misses. <tt>oprofile</tt> shows us the cache misses that occurred in the L2 as a result of instructions and data misses, whereas cachegrind helpfully splits it up for us.

On the Pentium-III, there are a similar series of events to monitor the instruction cache. For the L1 instruction cache (what the Pentium-III calls the "IFU"), we can measure the number of reads (or fetches) and misses directly <a name="iddle1354"></a><a name="iddle1355"></a><a name="iddle1356"></a><a name="iddle1357"></a>by using the following <a name="iddle1358"></a><a name="iddle1359"></a><a name="iddle1360"></a><a name="iddle1361"></a>events:

<pre>[ezolt@localhost book]$ op_help

...

IFU_IFETCH: number of non/cachable instruction fetches

IFU_IFETCH_MISS: number of instruction fetch misses

...

</pre>

We can also measure the number of instructions that were fetched from the L2 cache by using the following event:

<pre>[ezolt@localhost book]$ op_help

...

L2_IFETCH: (counter: 0, 1)

        number of L2 instruction fetches (min count: 500)

        Unit masks

        ----------

        0x08: (M)odified cache state

        0x04: (E)xclusive cache state

        0x02: (S)hared cache state

        0x01: (I)nvalid cache state

        0x0f: All cache states

...

</pre>

Unfortunately, as mentioned previously, the processor shares the L2 cache with the instruction and data, so there is no way to distinguish cache misses from data usage and instruction usage. We can use these events to approximate the same information that <tt>cachegrind</tt> provided.

If it is so difficult to extract the same information, why use <tt>oprofile</tt> at all? First, <tt>oprofile</tt> is much lower overhead (< 10 percent) and can be run on production applications. Second, <tt>oprofile</tt> can extract the exact events that are happening. This is much better than a possibly inaccurate simulator that does not take into account cache usage by the operating system or other applications.

Although these events are available on the Pentium-III, they are not necessarily available on any other processors. Each family of Intel and AMD processors has a different set of events that can be used to reveal different amounts of information about performance of the memory subsystem. <tt>op_help</tt> shows the events that can be monitored, but it might require reading Intel's or AMD's detailed processor information to understand what they mean.

To understand how you can use <tt>oprofile</tt> to extract cache information, compare the cache usage statistics of an application using both the virtual CPU of <tt>cachegrind</tt> and the actual CPU with <tt>oprofile</tt>. Let's run the burn program that we have been using as an example. Once again, it is an application that executes ten times the number of instructions in function <tt>a()</tt> as in function <tt>b()</tt>. It also accesses ten times the amount of data in function <tt>a()</tt> as in function <tt>b()</tt>. Here is the output of <tt>cachegrind</tt> for this demo <a name="iddle1362"></a><a name="iddle1363"></a><a name="iddle1364"></a><a name="iddle1365"></a>application:

<pre>---------------------------------------------------------------------------------------------

         Ir I1mr I2mr          Dr        D1mr  D2mr        Dw    D1mw    D2mw

---------------------------------------------------------------------------------------------

883,497,211  215  214 440,332,658 110,000,288 1,277 2,610,954 312,534 312,533  PROGRAM TOTALS

---------------------------------------------------------------------------------------------

         Ir I1mr I2mr          Dr        D1mr D2mr        Dw    D1mw    D2mw  file:function

---------------------------------------------------------------------------------------------

800,900,011    2    2 400,300,003 100,000,000  989   100,004       0       0  ???:a

 80,090,011    2    2  40,030,003  10,000,000    0    10,004       0       0  ???:b

</pre>

In the next few examples, I run the data collection phase of <tt>oprofile</tt> multiple times. I use <tt>oprof_start</tt> to set up the events for the particular run, and then run the demo application. Because my CPU has only two counters, I have to do this multiple times. This means that different sets of events will be monitored during the different executions of the program. Because my application does not change how it executes from each run, each run should produce similar results. This is not necessarily true for a more complicated application, such as a Web server or database, each of which can dramatically change how it executes based on the requests made to it. However, for the simple test application, it works just <a name="iddle1366"></a><a name="iddle1367"></a><a name="iddle1368"></a><a name="iddle1369"></a>fine.

After I collect this sampling information, we use <tt>opreport</tt> to extract the collected information. As shown in [Listing 5.9](ch05lev1sec2.html#ch05ex09), we query <tt>oprofile</tt> about the amount of data memory references that were made and how many times there was a miss in the L1 data CPU (DCU). As <tt>cachegrind</tt> told us, ten times the number of both memory references and L1 data misses occur in <a name="iddle1370"></a><a name="iddle1371"></a><a name="iddle1372"></a><a name="iddle1373"></a>function <tt>a()</tt>.

<a name="ch05ex09"></a>

##### Listing 5.9\.

<pre>[ezolt@wintermute test_app]$ opreport -l ./burn

event:DATA_MEM_REFS,DCU_LINES_IN

CPU: PIII, speed 467.74 MHz (estimated)

Counted DATA_MEM_REFS events (all memory references, cachable and non)

with a unit mask of 0x00 (No unit mask) count 233865

Counted DCU_LINES_IN events (total lines allocated in the DCU) with a

unit mask of 0x00 (No unit mask) count 23386

vma      samples  %           samples  %           symbol name

08048348 3640     90.8864     5598     90.9209     a

0804839e 365       9.1136     559       9.0791     b

</pre>

Now look at [Listing 5.10](ch05lev1sec2.html#ch05ex10), which shows <tt>opreport</tt> examining similar information for the instruction cache. Notice that the instructions executed in function <tt>a()</tt> are ten times the number as those in function <tt>b()</tt>, as we expect. However, notice that the number of L1 I misses differ from what <tt>cachegrind</tt> predicts. It is most likely that other applications and the kernel are polluting the cache and causing burn to miss in the <tt>icache</tt>. (Remember that <tt>cachegrind</tt> does not take kernel or other application cache usage into account.) This also probably happened with the data cache, but because the number of data cache misses caused by the application were so high, the extra events were lost in the <a name="iddle1374"></a><a name="iddle1375"></a><a name="iddle1376"></a><a name="iddle1377"></a>noise.

<a name="ch05ex10"></a>

##### Listing 5.10\.

<pre>[ezolt@wintermute test_app]$ opreport -l ./burn

event:IFU_IFETCH,IFU_IFETCH_MISS

CPU: PIII, speed 467.74 MHz (estimated)

Counted IFU_IFETCH events (number of non/cachable instruction fetches)

with a unit mask of 0x00 (No unit mask) count 233870

Counted IFU_IFETCH_MISS events (number of instruction fetch misses) with

a unit mask of 0x00 (No unit mask) count 500

vma      samples  %           samples  %           symbol name

08048348 8876     90.9240     14       93.3333      a

0804839e 886       9.0760     1         6.6667      b

</pre>

As you can see when comparing the output of <tt>cachegrind</tt> and <tt>oprofile</tt>, using <tt>oprofile</tt> to gather information about memory information is powerful because <tt>oprofile</tt> is low overhead and uses the processor hardware directly, but it can be difficult to find events that match those that you are <a name="iddle1378"></a><a name="iddle1379"></a><a name="iddle1380"></a><a name="iddle1381"></a>interested in.

<a name="ch05lev2sec7"></a>

#### 5.2.7\. ipcs

<tt>ipcs</tt> is a tool <a name="iddle1382"></a><a name="iddle1383"></a><a name="iddle1384"></a><a name="iddle1385"></a>that shows information about the system-wide interprocess communication memory. Processes can allocate system-wide shared memory, semaphores, or memory queues that can be shared by multiple processes running on the system. <tt>ipcs</tt> is best used to track down which applications are allocating and using large amounts of shared memory.

<a name="ch05lev3sec13"></a>

##### 5.2.7.1 Memory Performance-Related Options

<tt>ipcs</tt> is invoked with the following command line:

<pre>ipcs [-t] [-c] [-l] [-u] [-p]

</pre>

If <tt>ipcs</tt> is invoked without any parameters, it gives a summary of all the shared memory on the system. This includes information about the owner and size of the shared memory segment. [Table 5-6](ch05lev1sec2.html#ch05table06) describes options that cause <tt>ipcs</tt> to display different types information about the shared memory in the <a name="iddle1386"></a><a name="iddle1387"></a><a name="iddle1388"></a><a name="iddle1389"></a>system.

<a name="ch05table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 5-6\. <span class="docEmphasis"><tt>ipcs</tt></span> Command-Line Options

</caption><colgroup><col width="80"><col width="420"></colgroup>

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

<tt>-t</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1390"></a>This shows the time when the shared memory was created, when a process last attached to it, and when a process last detached from it.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-u</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1391"></a>This provides a summary about how much shared memory is being used and whether it has been swapped or is in memory.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-l</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1392"></a>This shows the system-wide limits for shared memory usage.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1393"></a>This shows the PIDs of the processes that created and last used the shared memory segments.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>x</tt>

</td>

<td class="docTableCell" align="left" valign="top">

This shows users who are the creators and owners of the shared memory segments.

</td>

</tr>

</tbody>

</table>

Because shared memory is used by multiple processes, it cannot be attributed to any particular process. <tt>ipcs</tt> provides enough information about the state of the system-wide shared memory to determine which processes allocated the shared memory, which processes are using it, and how often they are using it. This information proves useful when trying to reduce shared memory <a name="iddle1394"></a><a name="iddle1395"></a><a name="iddle1396"></a><a name="iddle1397"></a>usage.

<a name="ch05lev3sec14"></a>

##### 5.2.7.2 Example Usage

First, in <a name="iddle1398"></a><a name="iddle1399"></a><a name="iddle1400"></a><a name="iddle1401"></a>[Listing 5.11](ch05lev1sec2.html#ch05ex11), we ask <tt>ipcs</tt> how much of the system memory is being used for shared memory. This is a good overall indication of the state of shared memory in the system.

<a name="ch05ex11"></a>

##### Listing 5.11\.

<pre>[ezolt@wintermute tmp]$ ipcs -u

------ Shared Memory Status --------

segments allocated 21

pages allocated 1585

pages resident  720

pages swapped   412

Swap performance: 0 attempts     0 successes

------ Semaphore Status --------

used arrays = 0

allocated semaphores = 0

------ Messages: Status --------

allocated queues = 0

used headers = 0

used space = 0 bytes

</pre>

In this case, we can see that 21 different segments or pieces of shared memory have been allocated. All these segments consume a total of 1,585 pages of memory; 720 of these exist in physical memory and 412 have been swapped to disk.

Next, in [Listing 5.12](ch05lev1sec2.html#ch05ex12), we ask <tt>ipcs</tt> for a general overview of all the shared memory segments in the system. This indicates who is using each memory segment. In this case, we see a list of all the shared segments. For one in particular, the one with a share memory ID of 65538, the user (<tt>ezolt</tt>) is the owner. It has a permission of 600 (a typical UNIX permission), which in this case, means that only <tt>ezolt</tt> can read and write to it. It has 393,216 bytes, and 2 processes are attached <a name="iddle1402"></a><a name="iddle1403"></a><a name="iddle1404"></a><a name="iddle1405"></a>to it.

<a name="ch05ex12"></a>

##### Listing 5.12\.

<pre>[ezolt@wintermute tmp]$ ipcs

------ Shared Memory Segments --------

key        shmid      owner      perms      bytes      nattch     status

0x00000000 0          root      777        49152      1

0x00000000 32769      root      777        16384      1

0x00000000 65538      ezolt     600        393216     2          dest

0x00000000 98307      ezolt     600        393216     2          dest

0x00000000 131076     ezolt     600        393216     2          dest

0x00000000 163845     ezolt     600        393216     2          dest

0x00000000 196614     ezolt     600        393216     2          dest

0x00000000 229383     ezolt     600        393216     2          dest

0x00000000 262152     ezolt     600        393216     2          dest

0x00000000 294921     ezolt     600        393216     2          dest

0x00000000 327690     ezolt     600        393216     2          dest

0x00000000 360459     ezolt     600        393216     2          dest

0x00000000 393228     ezolt     600        393216     2          dest

0x00000000 425997     ezolt     600        393216     2          dest

0x00000000 458766     ezolt     600        393216     2          dest

0x00000000 491535     ezolt     600        393216     2          dest

0x00000000 622608     ezolt     600        393216     2          dest

0x00000000 819217     root      644        110592     2          dest

0x00000000 589842     ezolt     600        393216     2          dest

0x00000000 720916     ezolt     600        12288      2          dest

0x00000000 786454     ezolt     600        12288      2          dest

------ Semaphore Arrays --------

key        semid      owner      perms      nsems

------ Message Queues --------

key        msqid      owner      perms      used-bytes   messages

</pre>

Finally, we can figure out exactly which processes created the shared memory segments and which other processes are using them, as shown in [Listing 5.13](ch05lev1sec2.html#ch05ex13). For the segment with <tt>shmid 32769</tt>, we can see that the <tt>PID 1229</tt> created it and <a name="iddle1406"></a><a name="iddle1407"></a><a name="iddle1408"></a><a name="iddle1409"></a><tt>11954</tt> was the last to use it.

<a name="ch05ex13"></a>

##### Listing 5.13\.

<pre>[ezolt@wintermute tmp]$ ipcs -p

------ Shared Memory Creator/Last-op --------

shmid      owner      cpid       lpid

0          root       1224       11954

32769      root       1224       11954

65538      ezolt      1229       11954

98307      ezolt      1229       11954

131076     ezolt      1276       11954

163845     ezolt      1276       11954

196614     ezolt      1285       11954

229383     ezolt      1301       11954

262152     ezolt      1307       11954

294921     ezolt      1309       11954

327690     ezolt      1313       11954

360459     ezolt      1305       11954

393228     ezolt      1321       11954

425997     ezolt      1321       11954

458766     ezolt      1250       11954

491535     ezolt      1250       11954

622608     ezolt      1313       11954

819217     root       1224       11914

589842     ezolt      1432       14221

720916     ezolt      1250       11954

786454     ezolt      1313       11954

------ Message Queues PIDs --------

msqid      owner      lspid       lrpid

</pre>

After we have the PID responsible for the allocation and use, we can use a command such as <tt>ps -o command PID</tt> to track the PID back to the process name.

If shared memory usage becomes a significant amount of the system total, <tt>ipcs</tt> is a good way to track down the exact programs that are creating and using <a name="iddle1410"></a><a name="iddle1411"></a><a name="iddle1412"></a><a name="iddle1413"></a>the shared memory.

<a name="ch05lev2sec8"></a>

#### 5.2.8\. Dynamic Languages (Java, Mono)

As with <a name="iddle1414"></a><a name="iddle1415"></a><a name="iddle1416"></a><a name="iddle1417"></a><a name="iddle1418"></a><a name="iddle1419"></a><a name="iddle1420"></a><a name="iddle1421"></a><a name="iddle1422"></a><a name="iddle1423"></a>the CPU performance tools, most of the tools discussed in this chapter support analysis of static languages such as C and C++. Of the tools that we investigated, only <tt>ps</tt>, <tt>/proc</tt>, and <tt>ipcs</tt> work with dynamic languages such as Java, Mono, Python, and Perl. The cache and memory-profiling tools, such as <tt>oprofile</tt>, <tt>cachegrind</tt>, and <tt>memprof</tt>, do not. As with CPU profiling, each of these languages provides custom tools to extract information about memory usage.

For Java applications, if the <tt>java</tt> command is run with the <tt>-Xrunhprof</tt> command-line option, it profiles the application's memory usage. You can find more details at [http://antprof.sourceforge.net/hprof.html](http://antprof.sourceforge.net/hprof.html) or by running the <tt>java</tt> command with the <tt>-Xrunhprof:help</tt> option. For Mono applications, if the <tt>mono</tt> executable is passed the <tt>--profile</tt> flag, it also profiles the memory usage of the application. You can find more details about this <tt>at</tt> [http://www.go-mono.com/performance.html](http://www.go-mono.com/performance.html). Perl and Python do not appear to have <a name="iddle1424"></a><a name="iddle1425"></a><a name="iddle1426"></a><a name="iddle1427"></a><a name="iddle1428"></a><a name="iddle1429"></a><a name="iddle1430"></a><a name="iddle1431"></a><a name="iddle1432"></a><a name="iddle1433"></a>similar functionality.