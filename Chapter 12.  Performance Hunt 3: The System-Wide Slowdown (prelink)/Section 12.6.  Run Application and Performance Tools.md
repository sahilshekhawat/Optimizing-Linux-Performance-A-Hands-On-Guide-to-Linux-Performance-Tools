### 12.6\. Run Application and Performance Tools

Now we can finally <a name="iddle2724"></a><a name="iddle2725"></a><a name="iddle2726"></a><a name="iddle2727"></a><a name="iddle2728"></a><a name="iddle2729"></a><a name="iddle2730"></a>begin to analyze the performance characteristics of the different modes of <tt>prelink</tt>. As you just saw, <tt>prelink</tt> does not spend much time using the CPU; instead, it spends all of its time on disk I/O. Because <tt>prelink</tt> must call the kernel for disk I/O, we should be able to trace its execution using the <tt>strace</tt> performance tool. Because the quick mode of <tt>prelink</tt> does not appear to be that much faster than the standard <tt>full-run</tt> mode, we compare both runs using <tt>strace</tt> to see whether any suspicious behavior shows up.

At first, we ask <tt>strace</tt> to trace the slower full run of <tt>prelink</tt>. This is the run that creates the initial cache that is used when <tt>prelink</tt> is running in quick mode. Initially, we ask <tt>strace</tt> to show us the summary of the system calls that <tt>prelink</tt> made and see how long each took to complete. The command to do this is <a name="iddle2731"></a><a name="iddle2732"></a><a name="iddle2733"></a><a name="iddle2734"></a><a name="iddle2735"></a><a name="iddle2736"></a><a name="iddle2737"></a>shown in [Listing 12.7](ch12lev1sec6.html#ch12ex07).

<a name="ch12ex07"></a>

##### Listing 12.7\.

<pre>[root@localhost prelink]# strace -c -o af_sum  /usr/sbin/prelink -af

....

/usr/sbin/prelink: /usr/libexec/autopackage/luau-downloader.bin: Could

not parse '/usr/libexec/autopackage/luau-downloader.bin: error while

loading shared libraries: libuau.so.2: cannot open shared object file: No

such file or directory'

...

/usr/sbin/prelink: /usr/lib/mozilla-1.6/regchrome: Could not parse

'/usr/lib/mozilla-1.6/regchrome: error while loading shared libraries:

libxpcom.so: cannot open shared object file: No such file or  directory'

...

</pre>

[Listing 12.7](ch12lev1sec6.html#ch12ex07) is also a sample of prelink's output. <tt>prelink</tt> is struggling when trying to <tt>prelink</tt> some of the system executables and libraries. This information becomes valuable later, so remember it.

[Listing 12.8](ch12lev1sec6.html#ch12ex08) shows the summary output file that the <tt>strace</tt> command <a name="iddle2738"></a><a name="iddle2739"></a><a name="iddle2740"></a><a name="iddle2741"></a><a name="iddle2742"></a><a name="iddle2743"></a><a name="iddle2744"></a>in [Listing 12.7](ch12lev1sec6.html#ch12ex07) generated.

<a name="ch12ex08"></a>

##### Listing 12.8\.

<pre>[root@localhost prelink] # cat af_sum

execve("/usr/sbin/prelink", ["/usr/sbin/prelink", "-af"], [/* 31 vars

*/]) = 0

% time     seconds  usecs/call     calls     errors syscall

------ ----------- ----------- --------- --------- ----------------

 77.87  151.249181          65   2315836            read

 11.93   23.163231          55    421593            pread

  3.59    6.976880          63    110585            pwrite

  1.70    3.294913          17    196518            mremap

  1.02    1.977743          32     61774            lstat64

  0.97    1.890977          40     47820         1  open

  0.72    1.406801         249      5639            vfork

  0.35    0.677946          11     59097            close

...

------ ----------- ----------- --------- --------- ----------------

100.00  194.230415               3351032      5650 total

</pre>

As you can see in [Listing 12.8](ch12lev1sec6.html#ch12ex08), a significant amount of time is spent in the <tt>read</tt> system call. This is expected. <tt>prelink</tt> needs to figure out what shared libraries are linked into the application, and this requires that part of the executable be read in to be analyzed. The <tt>prelink</tt> documentation mentions that when generating the list of libraries that an application requires, that application is actually started by the dynamic loader in a special mode, and then the information is read from the executable using a pipe. This is why <tt>pread</tt> is also high in the profile. In contrast, we would expect the quick version to have very few of these calls.

To see how the profile of the quick version is different, we run the same <tt>strace</tt> command on the quick version of <tt>prelink</tt>. We can do that with the <a name="iddle2745"></a><a name="iddle2746"></a><a name="iddle2747"></a><a name="iddle2748"></a><a name="iddle2749"></a><a name="iddle2750"></a><a name="iddle2751"></a><tt>strace</tt> command shown in [Listing 12.9](ch12lev1sec6.html#ch12ex09).

<a name="ch12ex09"></a>

##### Listing 12.9\.

<pre>[root@localhost prelink]# strace -c -o aq_sum /usr/sbin/prelink -aq

</pre>

[Listing 12.10](ch12lev1sec6.html#ch12ex10) shows the <tt>strace</tt> profile of <tt>prelink</tt> running in quick mode.

<a name="ch12ex10"></a>

##### Listing 12.10\.

<pre>[root@localhost prelink] # cat aq_sum

execve("/usr/sbin/prelink", ["/usr/sbin/prelink", "-aq"], [/* 31 vars*/]) = 0

% time     seconds  usecs/call     calls     errors syscall

------ ----------- ----------- --------- --------- ----------------

 47.42    3.019337          70     43397            read

 26.74    1.702584          28     59822            lstat64

 10.35    0.658760         163      4041            getdents64

  5.52    0.351326          30     11681            pread

  3.26    0.207800          21      9678         1  open

  1.99    0.126593          21      5980        10  stat64

  1.98    0.126243          12     10155            close

  0.62    0.039335         165       239            vfork

....

------ ----------- ----------- ----------- --------- ------------

100.00    6.367230                  154681        250 total

</pre>

As expected, [Listing 12.10](ch12lev1sec6.html#ch12ex10) shows that the quick mode executes a significant number of <tt>lstat64</tt> system calls. These are the system calls that return the <tt>mtime</tt> and <tt>ctime</tt> for each executable. <tt>prelink</tt> looks in its cache to compare the saved <tt>mtime</tt> and <tt>ctime</tt> with the executable's current <tt>mtime</tt> and <tt>ctime</tt>. If the executable has changed, it starts to <tt>prelink</tt> it; if it has not changed, it continues to the next executable. The fact that <tt>prelink</tt> calls <tt>lstat64</tt> a large number of times is a good sign, because that means that <tt>prelink</tt>'s cache is working. However, the fact that <tt>prelink</tt> still calls <tt>read</tt> a large number of times is a bad sign. The cache should remember that the executables have already been prelinked and should not try to analyze them. We have to figure out why <tt>prelink</tt> is trying to analyze them. The easiest way to do that is to run <tt>strace</tt> in normal mode. <tt>strace</tt> will show all the system calls that <tt>prelink</tt> makes, and will hopefully clarify which files are being read and explain why <tt>read</tt> is being called so often. [Listing 12.11](ch12lev1sec6.html#ch12ex11) shows the command <tt>strace</tt> used on the quick <tt>prelink</tt>.

<a name="ch12ex11"></a>

##### Listing 12.11\.

<pre>[root@localhost prelink]# strace -o aq_run /usr/sbin/prelink -aq

</pre>

The <a name="iddle2752"></a><a name="iddle2753"></a><a name="iddle2754"></a><a name="iddle2755"></a><a name="iddle2756"></a><a name="iddle2757"></a><a name="iddle2758"></a>output of <tt>strace</tt> is a 14MB text file, <tt>aq_run</tt>. Browsing through it shows that <tt>prelink</tt> uses <tt>lstat64</tt> to check many of the libraries and executables. However, it reveals a few different types cases where <tt>read()</tt> is used. The first, shown in [Listing 12.12](ch12lev1sec6.html#ch12ex12), is where <tt>prelink</tt> reads a file that is a shell script. Because this shell script is not a binary ELF file, it can't be prelinked.

These shell scripts were unchanged since the original full-system <tt>prelink</tt> was run, so it would be nice if <tt>prelink</tt>'s cache would record the fact that this file cannot be prelinked. If the <tt>ctime</tt> and <tt>mtime</tt> do not change, <tt>prelink</tt> should not even try to read them. (If it was a shell script during the last full prelink and we haven't touched it, it still cannot be prelinked.)

<a name="ch12ex12"></a>

##### Listing 12.12\.

<pre>[root@localhost prelink] # cat aq_run

...

open("/bin/unicode_stop", O_RDONLY|O_LARGEFILE) = 5

read(5, "#!/bin/sh\n# stop u", 18)        = 18

close(5)                                  = 0

....

open("/bin/unicode_start", O_RDONLY|O_LARGEFILE) = 5

read(5, "#!/bin/bash\n# Enab", 18)       = 18

close(5)                                 = 0

....

</pre>

Next, in [Listing 12.13](ch12lev1sec6.html#ch12ex13), we <a name="iddle2759"></a><a name="iddle2760"></a><a name="iddle2761"></a><a name="iddle2762"></a><a name="iddle2763"></a>watch as <tt>prelink</tt> tries to operate on a statically linked application. Because this application does not rely on any shared libraries, it makes no sense to try to prelink it. The initial run of <tt>prelink</tt> should have caught the fact that this application could not be prelinked and stored that information in the <tt>prelink</tt> cache. In quick mode, it should not have even tried to prelink this binary.

<a name="ch12ex13"></a>

##### Listing 12.13\.

<pre>[root@localhost prelink] # cat aq_run

...

open("/bin/ash.static", O_RDONLY| O_LARGEFILE) = 5

read(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0", 18) = 18

fcntl64(5, F_GETFL)                     = 0x8000 (flags

O_RDONLY| O_LARGEFILE)

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0) = 16

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0) = 16

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0\3\0\1\0\0\0\0\201\4"...,

52, 0) = 52

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0\3\0\1\0\0\0\0\201\4"...,

52, 0) = 52

pread(5, "\1\0\0\0\0\0\0\0\0\200\4\10\0\200\4\10\320d\7\0\320d\7"...,

128, 52) = 128

pread(5, "\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0"...,

920, 488632) = 920

close(5)

...

</pre>

Finally, in <a name="iddle2764"></a><a name="iddle2765"></a><a name="iddle2766"></a><a name="iddle2767"></a><a name="iddle2768"></a>[Listing 12.14](ch12lev1sec6.html#ch12ex14), we see <tt>prelink</tt> reading a binary that it had trouble prelinking in the original full system run. We saw an error regarding this binary in the original <tt>prelink</tt> output. When it starts to read this file, it pulls in other libraries and begins to operate on each of those and their dependencies. This triggers an enormous amount of <a name="iddle2769"></a><a name="iddle2770"></a><a name="iddle2771"></a><a name="iddle2772"></a><a name="iddle2773"></a>reading.

<a name="ch12ex14"></a>

##### Listing 12.14\.

<a name="PLID7"></a>

<pre>[root@localhost prelink] # cat aq_run

...

lstat64("/usr/lib/mozilla-1.6/regchrome", {st_mode=S_IFREG|0755, st_size=14444,

...}) = 0

open("/usr/lib/mozilla-1.6/regchrome", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0", 18) = 18

fcntl64(6, F_GETFL)                     = 0x8000 (flags O_RDONLY|O_LARGEFILE)

pread(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0) = 16

...

open("/usr/lib/mozilla-1.6/libldap50.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                 = 0

lstat64("/usr/lib/mozilla-1.6/libgtkxtbin.so", {st_mode=S_IFREG|0755, st_size=14268, ...}) = 0

open("/usr/lib/mozilla-1.6/libgtkxtbin.so", O_RDONLY|O_LARGEFILE)  = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                = 0

lstat64("/usr/lib/mozilla-1.6/libjsj.so", {st_mode=S_IFREG|0755, st_size=96752,

...}) = 0

open("/usr/lib/mozilla-1.6/libjsj.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                 = 0

lstat64("/usr/lib/mozilla-1.6/mozilla-xremote-client", {st_mode=S_IFREG|0755,

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/ccc.gif) st_size=12896, ...}) = 0

lstat64("/usr/lib/mozilla-1.6/regxpcom", {st_mode=S_IFREG|0755, st_size=55144, ...}) = 0

lstat64("/usr/lib/mozilla-1.6/libgkgfx.so", {st_mode=S_IFREG|0755, st_size=143012, ...}) = 0

open("/usr/lib/mozilla-1.6/libgkgfx.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                 = 0

...

</pre>

Optimizing this case is tricky. Because this binary was not actually the problem (rather the library that it was linking to, <tt>libxpcom.so</tt>), we cannot just mark the executable as bad in the cache. However, if we store the errant library name <tt>libxpcom.so</tt> with the failing executable, it may be possible to check the times of the binary and the library, and only try to <tt>prelink</tt> again if one of them <a name="iddle2774"></a><a name="iddle2775"></a><a name="iddle2776"></a><a name="iddle2777"></a><a name="iddle2778"></a>has changed.