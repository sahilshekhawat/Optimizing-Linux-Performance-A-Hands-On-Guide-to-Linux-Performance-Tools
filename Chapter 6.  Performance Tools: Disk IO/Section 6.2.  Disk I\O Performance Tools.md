### 6.2\. Disk I/O Performance Tools

This section examines the various disk I/O performance tools that enable you to investigate how a given application is using the disk I/O subsystem, including how heavily each disk is being used, how well the kernel's disk cache is working, and which files a particular application has "open."

<a name="ch06lev2sec1"></a>

#### 6.2.1\. vmstat (ii)

As you saw in [Chapter 2](ch02.html#ch02), "[Performance Tools: System CPU](ch02.html#ch02)," <tt>vmstat</tt> is a great tool to give an overall view of how the system is performing. In addition to CPU and memory statistics, <tt>vmstat</tt> can provide a system-wide view of I/O performance.

<a name="ch06lev3sec1"></a>

##### 6.2.1.1 Disk I/O Performance-Related Options and Outputs

While using <tt>vmstat</tt> <a name="iddle1435"></a><a name="iddle1436"></a><a name="iddle1437"></a>to retrieve disk I/O statistics from the system, you must invoke it as follows:

<pre>vmstat [-D] [-d] [-p partition] [interval [count]]

</pre>

[Table 6-1](ch06lev1sec2.html#ch06table01) describes the other command-line parameters that influence the disk I/O statistics that vmstat will display.

<a name="ch06table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-1\. <span class="docEmphasis"><tt>vmstat</tt></span> Command-Line Options

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1438"></a><a name="iddle1439"></a><a name="iddle1440"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-D</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1441"></a>This displays Linux I/O subsystem total statistics. This option can give you a good idea of how your I/O subsystem is being used, but it won't give statistics on individual disks. The statistics given are the totals since system boot, rather than just those that occurred between this sample and the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1442"></a>This option displays individual disk statistics at a rate of one sample per <tt>interval</tt>. The statistics are the totals since system boot, rather than just those that occurred between this sample and the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p partition</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1443"></a>This displays performance statistics about the given partition at a rate of one sample per <tt>interval</tt>. The statistics are the totals since system boot, rather than just those that occurred between this sample and the previous sample.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>interval</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1444"></a>The length of time between samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>count</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1445"></a>The total number of samples to take.

</td>

</tr>

</tbody>

</table>

If you run <tt>vmstat</tt> without any parameters other than <tt>[interval]</tt> and <tt>[count]</tt>, it shows you the default output. This output contains three columns relevant to disk I/O performance: <tt>bo</tt>, <tt>bi</tt>, and <tt>wa</tt>. These <a name="iddle1446"></a><a name="iddle1447"></a><a name="iddle1448"></a>statistics are described in [Table 6-2](ch06lev1sec2.html#ch06table02).

<a name="ch06table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-2\. <span class="docEmphasis"><tt>vmstat</tt></span> I/O Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

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

<tt>bo</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1449"></a>This indicates the number of total blocks written to disk in the previous interval. (In <tt>vmstat</tt>, block size for a disk is typically 1,024 bytes.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>bi</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1450"></a>This shows the number of blocks read from the disk in the previous interval. (In <tt>vmstat</tt>, block size for a disk is typically 1,024 bytes.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wa</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1451"></a>This indicates the amount of CPU time spent waiting for I/O to complete. The rate of disk blocks written per second.

</td>

</tr>

</tbody>

</table>

When running with the <tt>-D</tt> mode, <tt>vmstat</tt> provides statistical information about the system's disk I/O system as a whole. Information about these statistics is provided in [Table 6-3](ch06lev1sec2.html#ch06table03). (Note that more information about these statistics is available in the Linux kernel source package, under <a name="iddle1452"></a><a name="iddle1453"></a><a name="iddle1454"></a><tt>Documentation/iostats.txt</tt>.)

<a name="ch06table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-3\. <span class="docEmphasis"><tt>vmstat</tt></span> Disk I/O Statistics

</caption><colgroup><col width="160"><col width="340"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1455"></a><a name="iddle1456"></a><a name="iddle1457"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>disks</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1458"></a>The total number of disks in the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>partitions</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1459"></a>The total number of partitions in the system.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>total reads</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1460"></a>The total number of reads that have been requested.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>merged reads</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1461"></a>The total number of times that different reads to adjacent locations on the disk were merged to improve performance.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>read sectors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1462"></a>The total number of sectors read from disk. (A sector is usually 512 bytes.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>milli reading</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1463"></a>The amount of time (in ms) spent reading from the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1464"></a>The total number of writes that have been requested.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>merged writes</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1465"></a>The total number of times that different writes to adjacent locations on the disk were merged to improve performance.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>written sectors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1466"></a>The total number of sectors written to disk. (A sector is usually 512 bytes.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>milli writing</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1467"></a>The amount of time (in ms) spent writing to the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>inprogress IO</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1468"></a>The total number of I/O that are currently in progress. Note that there is a bug in recent versions (v3.2) of <tt>vmstat</tt> in which this is incorrectly divided by 1,000, which almost always yields a 0.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>milli spent IO</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1469"></a>This is the number of milliseconds spent waiting for I/O to complete. Note that there is a bug in recent versions (v3.2) of <tt>vmstat</tt> in which this is the number of seconds spent on I/O rather than milliseconds.

</td>

</tr>

</tbody>

</table>

The <tt>-d</tt> option <a name="iddle1470"></a><a name="iddle1471"></a><a name="iddle1472"></a>of <tt>vmstat</tt> displays I/O statistics of each individual disk. These statistics are similar to those of the <tt>-D</tt> option and are described in [Table 6-4](ch06lev1sec2.html#ch06table04).

<a name="ch06table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-4\. <span class="docEmphasis"><tt>vmstat</tt></span> disk I/O Statistics

</caption><colgroup><col width="100"><col width="400"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1473"></a><a name="iddle1474"></a><a name="iddle1475"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>reads: total</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1476"></a>The total number of reads that have been requested.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>reads: merged</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1477"></a>The total number of times that different reads to adjacent locations on the disk were merged to improve performance.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>reads: sectors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1478"></a>The total number of sectors read from disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>reads: ms</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1479"></a>The amount of time (in ms) spent reading from the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes: total</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1480"></a>The total number of writes that have been requested for this disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes: merged</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1481"></a>The total number of times that different writes to adjacent locations on the disk were merged to improve performance.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes: sectors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1482"></a>The total number of sectors written to disk. (A sector is usually 512 bytes.)

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes: ms</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1483"></a>The amount of time (in ms) spent writing to the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>IO: cur</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1484"></a>The total number of I/O that are currently in progress. Note that there is a bug in recent versions of <tt>vmstat</tt> in which this is incorrectly divided by 1,000, which almost always yields a 0.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>IO: s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1485"></a>This is the number of seconds spent waiting for I/O to complete.

</td>

</tr>

</tbody>

</table>

Finally, when asked to provide <a name="iddle1486"></a><a name="iddle1487"></a><a name="iddle1488"></a>partition-specific statistics, <tt>vmstat</tt> displays those listed in [Table 6-5](ch06lev1sec2.html#ch06table05).

<a name="ch06table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-5\. <span class="docEmphasis"><tt>vmstat</tt></span> partition I/O Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

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

<tt>reads</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1489"></a>The total number of reads that have been requested for this partition.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>read sectors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1490"></a>The total number of sectors read from this partition.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>writes</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1491"></a>The total number of writes that resulted in I/O for this partition.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>requested writes</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1492"></a>The total number of reads that have been requested for this partition.

</td>

</tr>

</tbody>

</table>

The default <tt>vmstat</tt> output provides a coarse indication of system disk I/O, but a good level. The options provided by <tt>vmstat</tt> enable you to reveal more details about which device is responsible for the I/O. The primary advantage of <tt>vmstat</tt> over other I/O tools is that it is present on almost every Linux <a name="iddle1493"></a><a name="iddle1494"></a><a name="iddle1495"></a>distribution.

<a name="ch06lev3sec2"></a>

##### 6.2.1.2 Example Usage

The number <a name="iddle1496"></a><a name="iddle1497"></a><a name="iddle1498"></a>of I/O statistics that <tt>vmstat</tt> can present to the Linux user has been growing with recent releases of <tt>vmstat</tt>. The examples shown in this section rely on <tt>vmstat</tt> version 3.2.0 or greater. In addition, the extended disk statistics provided by <tt>vmstat</tt> are only available on Linux systems with a kernel version greater than 2.5.70.

In the first example, shown in [Listing 6.1](ch06lev1sec2.html#ch06ex01), we are just invoking <tt>vmstat</tt> for three samples with an interval of 1 second. <tt>vmstat</tt> outputs the system-wide performance overview that we saw in [Chapter 2](ch02.html#ch02).

<a name="ch06ex01"></a>

##### Listing 6.1\.

<pre>[ezolt@wintermute procps-3.2.0]$ ./vmstat 1 3

procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   swpd   free   buff  cache   si   so    bi    bo   in     cs us sy id wa

 1  1      0 197020  81804  29920    0    0   236    25 1017     67  1  1 93  4

 1  1      0 172252 106252  29952    0    0 24448     0 1200    395  1 36  0 63

 0  0      0 231068  50004  27924    0    0 19712    80 1179    345  1 34 15 49

</pre>

[Listing 6.1](ch06lev1sec2.html#ch06ex01) shows that during one of the samples, the system read 24,448 disk blocks. As mentioned previously, the block size for a disk is 1,024 bytes, so this means that the system is reading in data at about 23MB per second. We can also see that during this sample, the CPU was spending a significant portion of time waiting for I/O to complete. The CPU waits on I/O 63 percent of the time during the sample in which the disk was reading at ~23MB per second, and it waits on I/O 49 percent for the next sample, in which the disk was reading at ~19MB per second.

Next, in [Listing 6.2](ch06lev1sec2.html#ch06ex02), we ask <tt>vmstat</tt> to provide information about the I/O subsystem's performance since system <a name="iddle1499"></a><a name="iddle1500"></a><a name="iddle1501"></a>boot.

<a name="ch06ex02"></a>

##### Listing 6.2\.

<pre>[ezolt@wintermute procps-3.2.0]$ ./vmstat -D

            3 disks

            5 partitions

        <span class="docEmphStrong">53256</span> total reads

       <span class="docEmphStrong">641233</span> merged reads

      <span class="docEmphStrong">4787741</span> read sectors

       <span class="docEmphStrong">343552</span> milli reading

        14479 writes

        17556 merged writes

       257208 written sectors

      7237771 milli writing

            0 inprogress IO

          342 milli spent IO

</pre>

In [Listing 6.2](ch06lev1sec2.html#ch06ex02), <tt>vmstat</tt> provides I/O statistic totals for all the disk devices in the system. As mentioned previously, when reading and writing to a disk, the Linux kernel tries to merge requests for contiguous regions on the disk for a performance increase; <tt>vmstat</tt> reports these events as <tt>merged reads</tt> and <tt>merged writes</tt>. In this example, a large number of the reads issued to the system were merged before they were issued to the device. Although there were ~640,000 merged reads, only ~53,000 read commands were actually issued to the drives. The output also tells us that a total of 4,787,741 sectors have been read from the disk, and that since system boot, 343,552ms (or 344 seconds) were spent reading from the disk. The same statistics are available for write performance. This view of I/O statistics is a good view of the overall I/O subsystem's performance.

Although the previous example displayed I/O statistics for the entire system, the following example in [Listing 6.3](ch06lev1sec2.html#ch06ex03) shows the statistics broken down <a name="iddle1502"></a><a name="iddle1503"></a><a name="iddle1504"></a>for each individual disk.

<a name="ch06ex03"></a>

##### Listing 6.3\.

<pre>[ezolt@wintermute procps-3.2.0]$ ./vmstat -d 1 3

disk ----------reads------------ -----------writes----------- -------IO-------

     total merged sectors     ms  total merged sectors     ms    cur      s

fd0      0      0      0      0      0      0      0      0      0     0

hde  <span class="docEmphStrong">17099</span> 163180 <span class="docEmphStrong">671517</span> 125006   8279   9925 146304 2831237      0    125

hda      0      0      0      0      0      0      0      0      0     0

fd0      0      0      0      0      0      0      0      0      0     0

hde  <span class="docEmphStrong">17288</span> 169008 <span class="docEmphStrong">719645</span> 125918   8279   9925 146304 2831237      0    126

hda      0      0      0      0      0      0      0      0      0     0

fd0      0      0      0      0      0      0      0      0      0     0

hde  17288 169008 719645 125918   8290   9934 146464 2831245      0    126

hda      0      0      0      0      0      0      0      0      0     0

</pre>

[Listing 6.4](ch06lev1sec2.html#ch06ex04) shows that 60 (19,059 – 18,999) reads and 94 writes (24,795 – 24,795) have been issued to partition hde3\. This view can prove particularly useful if you are trying to determine which partition of a disk is seeing the most usage.

<a name="ch06ex04"></a>

##### Listing 6.4\.

<pre>[ezolt@wintermute procps-3.2.0]$ ./vmstat -p hde3 1 3

hde3          reads   read sectors  writes    requested writes

               <span class="docEmphStrong">18999</span>     191986      <span class="docEmphStrong">24701</span>     197608

               <span class="docEmphStrong">19059</span>     192466      <span class="docEmphStrong">24795</span>     198360

	       19161     193282      24795     198360

</pre>

Although <tt>vmstat</tt> provides statistics about individual disks/partitions, it only provides totals rather than the rate of change during the sample. This can make it difficult to eyeball which device's statistics have changed significantly from <a name="iddle1505"></a><a name="iddle1506"></a><a name="iddle1507"></a>sample to sample.

<a name="ch06lev2sec2"></a>

#### 6.2.2\. iostat

<tt>iostat</tt> is like <a name="iddle1508"></a><a name="iddle1509"></a><a name="iddle1510"></a><tt>vmstat</tt>, but it is a tool dedicated to the display of the disk I/O subsystem statistics. <tt>iostat</tt> provides a per-device and per-partition breakdown of how many blocks are written to and from a particular disk. (Blocks in <tt>iostat</tt> are usually sized at 512 bytes.) In addition, <tt>iostat</tt> can provide extensive information about how a disk is being utilized, as well as how long Linux spends waiting to submit requests to the disk.

<a name="ch06lev3sec3"></a>

##### 6.2.2.1 Disk I/O Performance-Related Options and Outputs

<tt>iostat</tt> is invoked using the following command line:

<pre>iostat [-d] [-k] [-x] [device] [interval [count]]

</pre>

Much like <tt>vmstat</tt>, <tt>iostat</tt> can display performance statistics at regular intervals. Different options modify the statistics that <tt>iostat</tt> displays. These options <a name="iddle1511"></a><a name="iddle1512"></a><a name="iddle1513"></a>are described in [Table 6-6](ch06lev1sec2.html#ch06table06).

<a name="ch06table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-6\. <span class="docEmphasis"><tt>iostat</tt></span> Command-Line Options

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

<tt>-d</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1514"></a>This displays only information about disk I/O rather than the default display, which includes information about CPU usage as well.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-k</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1515"></a>This shows statistics in kilobytes rather than blocks.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-x</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1516"></a>This shows extended-performance I/O statistics.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>device</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1517"></a>If a device is specified, <tt>iostat</tt> shows only information about that device.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>interval</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1518"></a>The length of time between samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>count</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1519"></a>The total number of samples to take.

</td>

</tr>

</tbody>

</table>

<a name="iddle1520"></a><a name="iddle1521"></a><a name="iddle1522"></a>The default output of <tt>iostat</tt> displays the performance statistics described in [Table 6-7](ch06lev1sec2.html#ch06table07).

<a name="ch06table07"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-7\. <span class="docEmphasis"><tt>iostat</tt></span> Device Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1523"></a><a name="iddle1524"></a><a name="iddle1525"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>tps</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1526"></a>Transfers per second. This is the number of reads and writes to the drive/partition per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Blk_read/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1527"></a>The rate of disk blocks read per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Blk_wrtn/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1528"></a>The rate of disk blocks written per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Blk_read</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1529"></a>The total number of blocks read during the interval.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>Blk_wrtn</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1530"></a>The total number of blocks written during the interval.

</td>

</tr>

</tbody>

</table>

When you invoke <tt>iostat</tt> with the <tt>-x</tt> parameter, it displays extended statistics about the disk I/O subsystem. These extended statistics are described in [Table 6-8](ch06lev1sec2.html#ch06table08).

<a name="ch06table08"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-8\. <span class="docEmphasis"><tt>iostat</tt></span> Extended Disk Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1531"></a><a name="iddle1532"></a><a name="iddle1533"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rrqm/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1534"></a>The number of reads merged before they were issued to the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wrqm/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1535"></a>The number of writes merged before they were issued to the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>r/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1536"></a>The number of reads issued to the disk per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>w/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1537"></a>The number of writes issued to the disk per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rsec/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1538"></a>Disk sectors read per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wsec/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1539"></a>Disk sectors written per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rkB/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1540"></a>Kilobytes read from disk per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wkB/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1541"></a>Kilobytes written to disk per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>avgrq-sz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1542"></a>The average size (in sectors) of disk requests.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>avgqu-sz</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1543"></a>The average size of the disk request queue.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>await</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1544"></a>The average time (in ms) for a request to be completely serviced. This average includes the time that the request was waiting in the disk's queue plus the amount of time it was serviced by the disk.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>svctm</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1545"></a>The average service time (in ms) for requests submitted to the disk. This indicates how long on average the disk took to complete a request. Unlike <tt>await</tt>, it does not include the amount of time spent waiting in the queue.

</td>

</tr>

</tbody>

</table>

<tt>iostat</tt> is a helpful utility, providing the most complete view of disk I/O performance statistics of any that I have found so far. Although <tt>vmstat</tt> is present everywhere and provides some basic statistics, <tt>iostat</tt> is far more complete. If it is available and installed on your system, <tt>iostat</tt> should be the first tool to turn to when a system has a disk I/O performance <a name="iddle1546"></a><a name="iddle1547"></a><a name="iddle1548"></a>problem.

<a name="ch06lev3sec4"></a>

##### 6.2.2.2 Example Usage

[Listing 6.5](ch06lev1sec2.html#ch06ex05) shows <a name="iddle1549"></a><a name="iddle1550"></a><a name="iddle1551"></a>an example <tt>iostat</tt> run while a disk benchmark is writing a test file to the file system on the <tt>/dev/hda2</tt> partition. The first sample <tt>iostat</tt> displays is the total system average since system boot time. The second sample (and any that would follow) is the statistics from each 1-second interval.

<a name="ch06ex05"></a>

##### Listing 6.5\.

<pre>[ezolt@localhost sysstat-5.0.2]$ ./iostat -d 1 2

Linux 2.4.22-1.2188.nptl (localhost.localdomain)        05/01/2004

Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn

hda               7.18       121.12       343.87    1344206    3816510

hda1              0.00         0.03         0.00        316         46

hda2              7.09       119.75       337.59    1329018    3746776

hda3              0.09         1.33         6.28      14776      69688

hdb               0.00         0.00         0.00         16          0

Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn

hda             105.05         5.78     12372.56         16      34272

hda1              0.00         0.00         0.00          0          0

hda2            100.36         5.78     11792.06         16      32664

hda3              4.69         0.00       580.51          0       1608

hdb               0.00         0.00         0.00          0          0

</pre>

One interesting note in the preceding example is that <tt>/dev/hda3</tt> had a small amount of activity. In the system being tested, <tt>/dev/hda3</tt> is a swap partition. Any activity recorded from this partition is caused by the kernel swapping memory to disk. In this way, <tt>iostat</tt> provides an indirect method to determine how much disk I/O in the system is the result of <a name="iddle1552"></a><a name="iddle1553"></a><a name="iddle1554"></a>swapping.

[Listing 6.6](ch06lev1sec2.html#ch06ex06) shows the extended output of <tt>iostat</tt>.

<a name="ch06ex06"></a>

##### Listing 6.6\.

<pre>[ezolt@localhost sysstat-5.0.2]$ ./iostat -x -dk 1 5 /dev/hda2

Linux 2.4.22-1.2188.nptl (localhost.localdomain)        05/01/2004

Device:    rrqm/s wrqm/s   r/s   w/s  rsec/s  wsec/s    rkB/s     wkB/s

avgrq-sz avgqu-sz   await  svctm  %util

hda2        11.22  44.40  3.15  4.20  115.00  388.97    57.50    194.49

68.52     1.75  237.17  11.47   8.43

Device:    rrqm/s wrqm/s   r/s   w/s  rsec/s  wsec/s    rkB/s     wkB/s

avgrq-sz avgqu-sz   await  svctm  %util

hda2         0.00 1548.00  0.00 100.00    0.00 13240.00     0.00   6620.00

132.40    55.13  538.60  10.00 100.00

Device:    rrqm/s wrqm/s   r/s   w/s  rsec/s  wsec/s    rkB/s     wkB/s

avgrq-sz avgqu-sz   await  svctm  %util

hda2         0.00 1365.00  0.00 131.00    0.00 11672.00     0.00   5836.00

89.10    53.86  422.44   7.63 100.00

Device:    rrqm/s wrqm/s   r/s   w/s  rsec/s  wsec/s   rkB/s      wkB/s

avgrq-sz avgqu-sz   await  svctm  %util

hda2         0.00 1483.00  0.00 84.00    0.00 12688.00    0.00    6344.00

151.0     39.69  399.52  11.90 100.00

Device:    rrqm/s wrqm/s   r/s   w/s  rsec/s  wsec/s    rkB/s     wkB/s

avgrq-sz avgqu-sz   await  svctm  %util

hda2         0.00 2067.00  0.00 123.00    0.00 17664.00     0.00   8832.00

143.61    58.59  508.54   8.13 100.00

</pre>

In [Listing 6.6](ch06lev1sec2.html#ch06ex06), you <a name="iddle1555"></a><a name="iddle1556"></a><a name="iddle1557"></a>can see that the average queue size is pretty high (~237 to 538) and, as a result, the amount of time that a request must wait (~422.44ms to 538.60ms) is much greater than the amount of time it takes to service the request (7.63ms to 11.90ms). These high average service times, along with the fact that the utilization is 100 percent, show that the disk is completely saturated.

The extended <tt>iostat</tt> output provides so many statistics that it only fits on a single line in a very wide terminal. However, this information is nearly all that you need to identify a particular disk as a <a name="iddle1558"></a><a name="iddle1559"></a><a name="iddle1560"></a>bottleneck.

<a name="ch06lev2sec3"></a>

#### 6.2.3\. sar

As discussed <a name="iddle1561"></a><a name="iddle1562"></a><a name="iddle1563"></a>in [Chapter 2](ch02.html#ch02), "[Performance Tools: System CPU](ch02.html#ch02)," <tt>sar</tt> can collect the performance statistics of many different areas of the Linux system. In addition to CPU and memory statistics, it can collect information about the disk I/O subsystem.

<a name="ch06lev3sec5"></a>

##### 6.2.3.1 Disk I/O Performance-Related Options and Outputs

When using <tt>sar</tt> to monitor disk I/O statistics, you can invoke it with the <a name="iddle1564"></a><a name="iddle1565"></a><a name="iddle1566"></a>following command line:

<pre>sar -d [ interval [ count ] ]

</pre>

Typically, <tt>sar</tt> displays information about the CPU usage in a system; to display disk usage statistics instead, you must use the <tt>-d</tt> option. <tt>sar</tt> can only display disk I/O statistics with a kernel version higher than 2.5.70\. The statistics that it displays are described in <a name="iddle1567"></a><a name="iddle1568"></a><a name="iddle1569"></a>[Table 6-9](ch06lev1sec2.html#ch06table09).

<a name="ch06table09"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-9\. <span class="docEmphasis"><tt>sar</tt></span> Device Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1570"></a><a name="iddle1571"></a><a name="iddle1572"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>tps</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1573"></a>Transfers per second. This is the number of reads and writes to the drive/partition per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rd_sec/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1574"></a>Number of disk sectors read per second.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>wr_sec/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1575"></a>Number of disk sectors written per second.

</td>

</tr>

</tbody>

</table>

The number of sectors is taken directly from the kernel, and although it is possible for it to vary, the size is usually <a name="iddle1576"></a><a name="iddle1577"></a><a name="iddle1578"></a>512 bytes.

<a name="ch06lev3sec6"></a>

##### 6.2.3.2 Example Usage

In [Listing 6.7](ch06lev1sec2.html#ch06ex07), <tt>sar</tt> is used <a name="iddle1579"></a><a name="iddle1580"></a><a name="iddle1581"></a>to collect information about the I/O of the devices on the system. <tt>sar</tt> lists the devices by their major and minor number rather than their names.

<a name="ch06ex07"></a>

##### Listing 6.7\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -d 1 3

Linux 2.6.5 (wintermute.phil.org)       05/02/04

16:38:28          DEV       tps  rd_sec/s  wr_sec/s

16:38:29       dev2-0      0.00      0.00      0.00

16:38:29      dev33-0    115.15    808.08   2787.88

16:38:29     dev33-64      0.00      0.00      0.00

16:38:29       dev3-0      0.00      0.00      0.00

16:38:29          DEV       tps  rd_sec/s  wr_sec/s

16:38:30       dev2-0      0.00      0.00      0.00

16:38:30      dev33-0    237.00   1792.00      8.00

16:38:30     dev33-64      0.00      0.00      0.00

16:38:30       dev3-0      0.00      0.00      0.00

16:38:30          DEV       tps  rd_sec/s  wr_sec/s

16:38:31       dev2-0      0.00      0.00      0.00

16:38:31      dev33-0    201.00   1608.00      0.00

16:38:31     dev33-64      0.00      0.00      0.00

16:38:31       dev3-0      0.00      0.00      0.00

Average:          DEV       tps  rd_sec/s   wr_sec/s

Average:       dev2-0      0.00      0.00       0.00

Average:      dev33-0    184.62   1404.68     925.75

Average:     dev33-64      0.00      0.00       0.00

Average:       dev3-0      0.00      0.00       0.00

</pre>

<tt>sar</tt> has a limited number of disk I/O statistics when compared to <tt>iostat</tt>. However, the capability of <tt>sar</tt> to simultaneously record many different types of statistics may make up for these <a name="iddle1582"></a><a name="iddle1583"></a><a name="iddle1584"></a>shortcomings.

<a name="ch06lev2sec4"></a>

#### 6.2.4\. lsof (List Open Files)

<tt>lsof</tt> provides a <a name="iddle1585"></a><a name="iddle1586"></a><a name="iddle1587"></a>way to determine which processes have a particular file open. In addition to tracking down the user of a single file, <tt>lsof</tt> can display the processes using the files in a particular directory. It can also recursively search through an entire directory tree and list the processes using files in that directory tree. <tt>lsof</tt> can prove helpful when narrowing down which applications are generating I/O.

<a name="ch06lev3sec7"></a>

##### 6.2.4.1 Disk I/O Performance-Related Options and Outputs

You can invoke <tt>lsof</tt> with the following command line to investigate which files processes have open:

<pre>lsof [-r delay] [+D directory] [+d directory] [file]

</pre>

Typically, <tt>lsof</tt> displays which processes are using a given file. However, by using the <tt>+d</tt> and <tt>+D</tt> options, it is possible for <tt>lsof</tt> to display this information for more than one file. [Table 6-10](ch06lev1sec2.html#ch06table10) describes the command-line options of <tt>lsof</tt> that prove helpful when tracking down an I/O performance problem.

<a name="ch06table10"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-10\. <span class="docEmphasis"><tt>lsof</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1588"></a><a name="iddle1589"></a><a name="iddle1590"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-r delay</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1591"></a>This causes <tt>lsof</tt> to output statistics every <tt>delay</tt> seconds.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>+D directory</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1592"></a>This causes <tt>lsof</tt> to recursively search all the files in the given directory and report on which processes are using them.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>+d directory</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1593"></a>This causes <tt>lsof</tt> to report on which processes are using the files in the given directory.

</td>

</tr>

</tbody>

</table>

<a name="iddle1594"></a><a name="iddle1595"></a><a name="iddle1596"></a><tt>lsof</tt> displays the statistics described in [Table 6-11](ch06lev1sec2.html#ch06table11) when showing which processes are using the specified files.

<a name="ch06table11"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 6-11\. <span class="docEmphasis"><tt>lsof</tt></span> File Statistics

</caption><colgroup><col width="80"><col width="420"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1597"></a><a name="iddle1598"></a><a name="iddle1599"></a>Statistic

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>COMMAND</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1600"></a>The name of the command that has the file open.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>PID</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1601"></a>The PID of the command that has the file open.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>USER</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1602"></a>The user who has the file open.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>FD</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1603"></a>The file descriptor of the file, or <tt>tex</tt> for a executable, <tt>mem</tt> for a memory mapped file.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>TYPE</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1604"></a>The type of file. <tt>REG</tt> for a regular file.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>DEVICE</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1605"></a>Device number in major, minor number.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>SIZE</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1606"></a>The size of the file.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>NODE</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1607"></a>The inode of the file.

</td>

</tr>

</tbody>

</table>

Although <tt>lsof</tt> does not show the amount and type of file access that a particular process is doing, it at least displays which processes are using a particular <a name="iddle1608"></a><a name="iddle1609"></a><a name="iddle1610"></a>file.

<a name="ch06lev3sec8"></a>

##### 6.2.4.2 Example Usage

[Listing 6.8](ch06lev1sec2.html#ch06ex08) <a name="iddle1611"></a><a name="iddle1612"></a><a name="iddle1613"></a>shows <tt>lsof</tt> being run on the <tt>/usr/bin</tt> directory. This run shows which processes are accessing all of the files in <tt>/usr/bin</tt>.

<a name="ch06ex08"></a>

##### Listing 6.8\.

<pre>[ezolt@localhost manuscript]$  /usr/sbin/lsof -r 2 +D /usr/bin/

COMMAND    PID  USER  FD   TYPE DEVICE   SIZE   NODE NAME

gnome-ses 2162 ezolt txt    REG    3,2 113800 597490 /usr/bin/gnome-session

ssh-agent 2175 ezolt txt    REG    3,2  61372 596783 /usr/bin/ssh-agent

gnome-key 2182 ezolt txt    REG    3,2  77664 602727 /usr/bin/gnome-keyring-daemon

metacity  2186 ezolt txt    REG    3,2 486520 597321 /usr/bin/metacity

gnome-pan 2272 ezolt txt    REG    3,2 503100 602174 /usr/bin/gnome-panel

nautilus  2280 ezolt txt    REG    3,2 677812 598239 /usr/bin/nautilus

magicdev  2287 ezolt txt    REG    3,2  27008 598375 /usr/bin/magicdev

eggcups   2292 ezolt txt    REG    3,2  32108 599596 /usr/bin/eggcups

pam-panel 2305 ezolt txt    REG    3,2  45672 600140 /usr/bin/pam-panel-icon

<span class="docEmphStrong">gnome-ter 3807 ezolt txt    REG    3,2 289116 596834 /usr/bin/gnome-terminal</span>

less      6452 ezolt txt    REG    3,2 104604 596239 /usr/bin/less

=======

COMMAND    PID  USER  FD   TYPE DEVICE   SIZE   NODE NAME

gnome-ses 2162 ezolt txt    REG    3,2 113800 597490 /usr/bin/gnome-session

ssh-agent 2175 ezolt txt    REG    3,2  61372 596783 /usr/bin/ssh-agent

gnome-key 2182 ezolt txt    REG    3,2  77664 602727 /usr/bin/gnome-keyring-daemon

metacity  2186 ezolt txt    REG    3,2 486520 597321 /usr/bin/metacity

gnome-pan 2272 ezolt txt    REG    3,2 503100 602174 /usr/bin/gnome-panel

nautilus  2280 ezolt txt    REG    3,2 677812 598239 /usr/bin/nautilus

magicdev  2287 ezolt txt    REG    3,2  27008 598375 /usr/bin/magicdev

eggcups   2292 ezolt txt    REG    3,2  32108 599596 /usr/bin/eggcups

pam-panel 2305 ezolt txt    REG    3,2  45672 600140 /usr/bin/pam-panel-icon

gnome-ter 3807 ezolt txt    REG    3,2 289116 596834 /usr/bin/gnome-terminal

less      6452 ezolt txt    REG    3,2 104604 596239 /usr/bin/less

</pre>

In particular, we can see that process 3807 is using the file <tt>/usr/bin/gnome-terminal</tt>. This file is an executable, as indicated by the <tt>txt</tt> in the <tt>FD</tt> column, and the name of the command that is using it is <tt>gnome-terminal</tt>. This makes sense; the process that is running <tt>gnome-terminal</tt> must therefore have the executable open. One interesting thing to note is that this file is on the device 3,2, which corresponds to <tt>/dev/hda2</tt>. (You can figure out the device number for all the system devices by executing <tt>ls -la /dev</tt> and looking at the output field that normally displays size.) Knowing on which device a file is located can help if you know that a particular device is the source of an I/O bottleneck. <tt>lsof</tt> provides the unique ability to trace an open file descriptor back to individual processes; although it does not show which processes are using a significant amount of I/O, it does provide a starting <a name="iddle1614"></a><a name="iddle1615"></a><a name="iddle1616"></a>point.