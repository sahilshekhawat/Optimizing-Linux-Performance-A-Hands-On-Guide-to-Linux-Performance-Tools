### 12.3\. Find a Baseline/Set a Goal

Once again, the first <a name="iddle2669"></a><a name="iddle2670"></a>step is to determine the current state of the problem.

However, in this case, it is not so easy to do. We do not know when the problem will begin or how long it will last, so we cannot really set a baseline without more investigation. As far as a goal, ideally we would like the problem to disappear completely, but the problem might be caused by essential OS functions, so eliminating it entirely might not be possible.

First, we need to do a little more investigation into why this problem is happening to figure out a reasonable baseline. The initial step is to <a name="iddle2671"></a><a name="iddle2672"></a><a name="iddle2673"></a>run <tt>top</tt> as the slowdown is happening. This gives us a list of processes that may be causing the problem, or it may even point at the kernel itself.

In this case, as shown in [Listing 12.1](ch12lev1sec3.html#ch12ex01), we run <tt>top</tt> and ask it to show only nonidle <a name="iddle2674"></a><a name="iddle2675"></a>processes (by pressing <I> as <tt>top</tt> runs).

<a name="ch12ex01"></a>

##### Listing 12.1\.

<pre>top - 12:03:40 up 12 min,  7 users,  load average: 1.35, 0.98, 0.53

Tasks:  86 total,   2 running,  84 sleeping,   0 stopped,     0 zombie

Cpu(s):  2.3% us,  5.0% sy,  1.7% ni,  0.0% id, 91.0% wa,  0.0% hi,  0.0% si

Mem:    320468k total,   317024k used,     3444k free,    24640k buffers

Swap:   655192k total,        0k used,   655192k free,   183620k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND

 5458 root      34  19  4920 1944 2828 R  1.7  0.6   0:01.13 prelink

 5389 ezolt     17   0  3088  904 1620 R  0.7  0.3   0:00.70 top

</pre>

The <tt>top</tt> output in <a name="iddle2676"></a><a name="iddle2677"></a><a name="iddle2678"></a>[Listing 12.1](ch12lev1sec3.html#ch12ex01) has several interesting properties. First, we notice that no process is hogging the CPU; both nonidle tasks are using less than 2 percent of the total CPU time. Second, the system is spending 91 percent waiting for I/O to happen. Third, the system is not using any of the swap space, so the grinding disk is NOT caused by swapping. Finally, an unknown process, <tt>prelink</tt>, <a name="iddle2679"></a><a name="iddle2680"></a>is running when the problem happens. It is unclear what this <tt>prelink</tt> command is, so we will remember that application name and investigate it later.

Our next step is to run <a name="iddle2681"></a><a name="iddle2682"></a><a name="iddle2683"></a><tt>vmstat</tt> to see what the system is doing. [Listing 12.2](ch12lev1sec3.html#ch12ex02) shows the result of <tt>vmstat</tt> and confirms what we saw with t<tt>op</tt>. That is, ~90 percent of the time the system is waiting for I/O. It also tells us that the disk subsystem is reading in about 1,000 blocks a second of data. This is a significant amount of <a name="iddle2684"></a><a name="iddle2685"></a>disk I/O.

<a name="ch12ex02"></a>

##### Listing 12.2\.

<pre>[ezolt@localhost ezolt]$ vmstat 1 10

procs -----------memory---------- ---swap-- -----io----  --system-- ----cpu----

 r  b   swpd   free   buff  cache   si   so    bi    bo    in    cs us sy id wa

 0  1      0   2464  24568 184992    0    0   689    92  1067   337  5  4 45 46

 0  1      0   2528  24500 185060    0    0  1196     0  1104  1324  6 10  0 84

 0  1      0   3104  24504 184276    0    0   636   684  1068   967  3  7  0 90

 0  1      0   3160  24432 184348    0    0  1300     0  1096  1575  4 10  0 86

 0  2      0   3488  24336 184444    0    0  1024     0  1095  1498  5  9  0 86

 0  1      0   2620  24372 185188    0    0   980     0  1096  1900  6 12  0 82

 0  1      0   3704  24216 184304    0    0  1480     0  1120   500  1  7  0 92

 0  1      0   2296  24256 185564    0    0  1384   684  1240  1349  6  8  0 86

 2  1      0   3320  24208 184572    0    0   288     0  1211  1206 63  7  0 30

 0  1      0   3576  24148 184632    0    0  1112     0  1153   850 19  7  0 74

</pre>

Now that we know <a name="iddle2686"></a><a name="iddle2687"></a><a name="iddle2688"></a><a name="iddle2689"></a><a name="iddle2690"></a>that the disk is being heavily used, the kernel is spending a significant amount of time waiting for I/O, and an unknown application, <tt>prelink</tt>, is running, we can begin to figure out exactly what the system is doing.

We do not know for certain that <a name="iddle2691"></a><a name="iddle2692"></a><tt>prelink</tt> is causing the problem, but we suspect that it is. The easiest way to determine whether <tt>prelink</tt> is causing the disk I/O is to "kill" the <tt>prelink</tt> process and see whether the disk usage goes away. (This might not be possible on a production machine, but since we are working on a personal desktop we can be more fast and loose.) [Listing 12.3](ch12lev1sec3.html#ch12ex03) shows the output of <tt>vmstat</tt>, where halfway through this output, we killed the <tt>prelink</tt> process. As you can see, the blocks read in drop to zero after <tt>prelink</tt> is <a name="iddle2693"></a><a name="iddle2694"></a><a name="iddle2695"></a>killed.

<a name="ch12ex03"></a>

##### Listing 12.3\.

<pre>procs -----------memory---------- ---swap-- -----io---- --system-- ----cpu----

 r  b   swpd   free   buff  cache   si   so    bi    bo   in    cs us sy id wa

 0  1 122208   3420  13368  84508    0    0  1492   332 1258  1661 15 11  0 74

 0  1 122516   3508  13404  85780    0  308  1188   308 1134  1163  5  7  0 88

 0  2 123572   2616  13396  86860    0 1056  1420  1056 1092   911  4  6  0 90

 0  1 126248   3064  13356  86656    0 2676   316  2676 1040   205  1  2  0 97

 0  2 126248   2688  13376  87156    0    0   532   528 1057   708  2  5  0 93

 0  0 126248   3948  13384  87668    0    0   436     4 1043   342  3  3 43 51

 1  0 126248   3980  13384  87668    0    0     0     0 1154   426  3  1 96  0

 0  0 126248   3980  13384  87668    0    0     0     0 1139   422  2  1 97  0

12  0 126248   4020  13384  87668    0    0     0     0 1023   195  9  0 91  0

</pre>

Because <tt>prelink</tt> looks like the guilty application, we can start investigating exactly what it is and why it is run. In [Listing 12.4](ch12lev1sec3.html#ch12ex04), we ask rpm to tell us which files are part of the package that <tt>prelink</tt> is part <a name="iddle2696"></a><a name="iddle2697"></a><a name="iddle2698"></a><a name="iddle2699"></a>of.

<a name="ch12ex04"></a>

##### Listing 12.4\.

<pre>[root@localhost root]# rpm -qlf 'which prelink'

/etc/cron.daily/prelink

/etc/prelink.conf

/etc/rpm/macros.prelink

/etc/sysconfig/prelink

/usr/bin/execstack

/usr/sbin/prelink

/usr/share/doc/prelink-0.3.2

/usr/share/doc/prelink-0.3.2/prelink.pdf

/usr/share/man/man8/execstack.8.gz

/usr/share/man/man8/prelink.8.gz

</pre>

First, we note that the <tt>prelink</tt> package has a <tt>cron</tt> job that runs daily. This explains why the performance problem occurs periodically. Second, we note that <tt>prelink</tt> has a man page and documentation that describe its function. The man page describes <tt>prelink</tt> as an application that can <tt>prelink</tt> executables and libraries so that their startup times decrease. (It is just a little ironic that an application that is meant to boost performance is slowing down our system.) The <tt>prelink</tt> application can be run in two modes. The first mode causes all of the specified executables and libraries to be prelinked even if it has already been done. (This is specified by the <tt>--force</tt> or <tt>-f</tt> option). The second mode is a quick mode, where <tt>prelink</tt> just checks the <tt>mtimes</tt> and <tt>ctimes</tt> of the libraries and executables to see whether anything has changed since the last prelinking. (This is specified by the <tt>--quick</tt> or <tt>-q</tt> option.) Normally, <tt>prelink</tt> writes all the <tt>mtimes</tt> and <tt>ctimes</tt> of the prelinked executable to its own cache. It then uses that information in quick mode to avoid prelinking those executables that have already been <a name="iddle2700"></a><a name="iddle2701"></a><a name="iddle2702"></a><a name="iddle2703"></a>linked.

Examining the <tt>cron</tt> entry from the <tt>prelink</tt> package shows that, by default, the Fedora system uses <tt>prelink</tt> in both modes. It calls <tt>prelink</tt> in the full mode every 14 days. However, for every day between that, <tt>prelink</tt> runs in the quick mode.

Timing <tt>prelink</tt> in both full and quick mode tells us how slow the worst case is (full prelinking) and how much performance increases when using the quick mode. We have to be careful when timing <tt>prelink</tt>, because different runs may yield radically different times. When running an application that uses a significant amount of disk I/O, it is necessary to run it several times to get an accurate indication of its baseline performance. The first time a disk-intensive application is run, much of the data from its I/O is loaded into the cache. The second time the application is run, performance is much greater, because the data it is using is in the disk caches, and it does not need to read from the disk. If you use the first run as the baseline, you can be misled into believing that performance has increased after a performance tweak when the real cause of the performance boost was the warm caches. By just running the application several times, you can warm up the caches and get an accurate baseline. [Listing 12.5](ch12lev1sec3.html#ch12ex05) shows the results of <tt>prelink</tt> in both modes after it has been run several <a name="iddle2704"></a><a name="iddle2705"></a>times.

<a name="ch12ex05"></a>

##### Listing 12.5\.

<pre>[root@localhost root]# time prelink -f -a

....

real    4m24.494s

user    0m9.552s

sys     0m14.322s

[root@localhost root]# time prelink -q -a

....

real    3m18.136s

user    0m3.187s

sys     0m3.663s

</pre>

The first fact to note from [Listing 12.5](ch12lev1sec3.html#ch12ex05) is that the quick mode is not all that quicker than the full mode. This is suspicious and needs more investigation. The second fact reinforces what top reported. <tt>prelink</tt> spends only a small amount of CPU time; the rest is spent waiting for disk I/O.

Now we have to pick a reasonable goal. The PDF file that was installed in the <tt>prelink</tt> package describes the process of prelinking. It also says that the full mode should take several minutes, and the quick mode should take several seconds. As a goal, let's try to reduce the quick mode's time to under a minute. Even if we could optimize the quick mode, we would still have significant disk grinding every 14 days, but the daily runs would be much more <a name="iddle2706"></a><a name="iddle2707"></a><a name="iddle2708"></a><a name="iddle2709"></a>tolerable.