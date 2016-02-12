### 9.7\. Optimizing Disk I/O Usage

When you determine that disk I/O <a name="iddle2287"></a>is a problem, it can be helpful to determine which application is causing the I/O.

[Figure 9-5](ch09lev1sec7.html#ch09fig05) shows the steps we take to determine the cause of disk I/O usage.

<a name="ch09fig05"></a>

<center>

##### Figure 9-5\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig05.gif)

</center>

To begin the investigation, jump to [Section 9.7.1](ch09lev1sec7.html#ch09lev2sec32)

<a name="ch09lev2sec32"></a>

#### 9.7.1\. Is the System Stressing a Particular Disk?

Run <tt>iostat</tt> in <a name="iddle2288"></a>the extended statistic mode and look for partitions that have an average wait (<tt>await</tt>) greater than zero. <tt>await</tt> is the average number of milliseconds that requests are waiting to be filled. The higher this number, the more the disk is overloaded. You can confirm this overload by looking at the amount of read and write traffic on a disk and determining whether it is close to the maximum amount that the drive can handle.

If many files are accessed on a single drive, it may be possible to increase performance by spreading out these files to multiple disks. However, it is first necessary to determine what files are being <a name="iddle2289"></a>accessed.

Proceed to [Section 9.7.2](ch09lev1sec7.html#ch09lev2sec33).

<a name="ch09lev2sec33"></a>

#### 9.7.2\. Which Application Is Accessing the Disk?

As mentioned in <a name="iddle2290"></a>the chapter on disk I/O, this is where it can be difficult to determine which process is causing a large amount of I/O, so we must try to work around the lack of tools to do this directly. By running <tt>top</tt>, you first look for processes that are nonidle. For each of these processes, proceed to [Section 9.7.3](ch09lev1sec7.html#ch09lev2sec34).

<a name="ch09lev2sec34"></a>

#### 9.7.3\. Which Files Are Accessed by the Application?

First, use <tt>strace</tt> to <a name="iddle2291"></a>trace all the system calls that an application is making that have to do with file I/O, using <tt>strace -e trace=file</tt>. We can then <tt>strace</tt> using summary information to see how long each call is taking. If certain read and write calls are taking a long time to complete, this process may be the cause of the I/O slowdown. By running <tt>strace</tt> in normal mode, it is possible to see which file descriptors it is reading and writing from. To map these file descriptors back to files on a file system, we can look in the <tt>proc</tt> file system. The files in <tt>/proc/<pid>/fd/</tt> are symbolic links from the file descriptor number to the actual files. An <tt>ls -la</tt> of this directory shows which files this process is using. By knowing which files the process is accessing, it might be possible to reduce the amount of I/O the process is doing, spread it more evenly between multiple disks, or even move it to a faster disk.

After you determine which files the process is <a name="iddle2292"></a>accessing, go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).