### 9.8\. Optimizing Network I/O Usage

When you know that a network problem is happening, Linux provides a set of tools to determine which applications are involved. However, when you are connected to external machines, the fix to a network problem is not always within your control.

[Figure 9-6](ch09lev1sec8.html#ch09fig06) shows the steps that we take to investigate a network performance problem.

<a name="ch09fig06"></a>

<center>

##### Figure 9-6\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig06_alt.gif)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig06_alt.gif)

[To start the investigation, continue to](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig06_alt.gif) [Section 9.8.1](ch09lev1sec8.html#ch09lev2sec35).

<a name="ch09lev2sec35"></a>

#### 9.8.1\. Is Any Network Device Sending/Receiving Near the Theoretical Limit?

The first thing to <a name="iddle2293"></a>do is to use <tt>ethtool</tt> to determine what hardware speed each Ethernet device is set to. If you record this information, you then investigate whether any of the network devices are saturated. Ethernet devices and/or switches can be easily mis-configured, and <tt>ethtool</tt> shows what speed each device believes that it is operating at. After you determine the theoretical limit of each of the Ethernet devices, use <tt>iptraf</tt> (of even <tt>ifconfig</tt>) to determine the amount of traffic that is flowing over each interface. If any of the network devices appear to be saturated, go to [Section 9.8.3](ch09lev1sec8.html#ch09lev2sec37); otherwise, go to [Section 9.8.2](ch09lev1sec8.html#ch09lev2sec36).

<a name="ch09lev2sec36"></a>

#### 9.8.2\. Is Any Network Device Generating a Large Number of Errors?

Network traffic can <a name="iddle2294"></a>also appear to be slow because of a high number of network errors. Use <tt>ifconfig</tt> to determine whether any of the interfaces are generating a large number of errors. A large number of errors can be the result of a mismatched Ethernet card / Ethernet switch setting. Contact your network administrator, search the Web for people with similar problems, or e-mail questions to one of the Linux networking newsgroups.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec37"></a>

#### 9.8.3\. What Type of Traffic Is Running on That Device?

If a particular device is <a name="iddle2295"></a>servicing a large amount of data, use <tt>iptraf</tt> to track down what types of traffic that device is sending and receiving. When you know the type of traffic that the device is handling, advance to [Section 9.8.4](ch09lev1sec8.html#ch09lev2sec38).

<a name="ch09lev2sec38"></a>

#### 9.8.4\. Is a Particular Process Responsible for That Traffic?

Next, we want to <a name="iddle2296"></a>determine whether a particular process is responsible for that traffic. Use <tt>netstat</tt> with the <tt>-p</tt> switch to see whether any process is handling the type of traffic that is flowing over the network port.

If an application is responsible, go to [Section 9.8.6](ch09lev1sec8.html#ch09lev2sec40). If none are responsible, go to [Section 9.8.5](ch09lev1sec8.html#ch09lev2sec39).

<a name="ch09lev2sec39"></a>

#### 9.8.5\. What Remote System Is Sending the Traffic?

If no application is responsible <a name="iddle2297"></a>for this traffic, some system on the network may be bombarding your system with unwanted traffic. To determine which system is sending all this traffic, use <tt>iptraf</tt> or <tt>etherape</tt>.

If it is possible, contact the owner of this system and try to figure out why this is happening. If the owner is unreachable, it might be possible to set up <tt>ipfilters</tt> within the Linux kernel to always drop this particular traffic, or to set up a firewall between the remote machine and the local machine to intercept the <a name="iddle2298"></a>traffic.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).

<a name="ch09lev2sec40"></a>

#### 9.8.6\. Which Application Socket Is Responsible for the Traffic?

Determining <a name="iddle2299"></a>which socket is being used is a two-step process. First, we can use <tt>strace</tt> to trace all the I/O system calls that an application is making by using <tt>strace -e trace=file</tt>. This shows which file descriptors the process is reading and writing from. Second, we map these file descriptors back to a socket by looking in the <tt>proc</tt> file system. The files in <tt>/proc/<pid>/fd/</tt> are symbolic links from the file descriptor number to the actual files or sockets. An <tt>ls -la</tt> of this directory shows all the file descriptors of this particular process. Those with <tt>socket</tt> in the name are network sockets. You can then use this information to determine inside the program which socket is causing all the communication.

Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).