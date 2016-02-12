### 12.8\. Reporting the Problem

Because we have <a name="iddle2815"></a><a name="iddle2816"></a><a name="iddle2817"></a><a name="iddle2818"></a><a name="iddle2819"></a>found a problem and potential solution in a pretty low-level piece of system software, it is a good idea to work with the author to resolve the problem. We must at least submit a bug report so that the author knows that a problem exists. Submitting the tests we used to discover the problem helps him to reproduce the problem and hopefully fix it. In this case, we will add a bug report to Red Hat's bugzilla (bugzilla.redhat.com) tracking system. (Most other distributions have similar bug tracking systems.) Our bug report describes the problem that we encountered and the possible solution that we discovered.

When arriving at bugzilla, we first search for bug reports in <tt>prelink</tt> to see whether anyone else has reported this problem. In this case, no one has, so we enter the bug report in [Listing 12.22](ch12lev1sec8.html#ch12ex22) and wait for the author or maintainer to respond and possibly fix the <a name="iddle2820"></a><a name="iddle2821"></a><a name="iddle2822"></a><a name="iddle2823"></a><a name="iddle2824"></a>bug.

<a name="ch12ex22"></a>

##### Listing 12.22\.

<pre>From Bugzilla Helper:

User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.6)

Gecko/20040510

Description of problem:

When running in quick mode, prelink does not cache the fact that some

binaries can not be prelinked. As a result it rescans them every time ,

even if prelink is running in quick mode. This causes the disk to grind

and dramatically slows down the whole system.

There are 3 types of executables that it retries during quick mode:

1) Static Binaries

2) Shell Scripts

3) Binaries that rely on unprelinkable binaries. (Such as OpenGL)

For 1&2, it would be nice if prelink cached that fact that these

executables can not be prelinked, and then in quick mode check their

ctime & mtime, and don't even try to read them if it already knows that

they can't be prelinked.

For 3, it would be nice if prelink recorded which libraries are causing

the prelink to fail (Take the OpenGL case for example), and record that

with the binary in the cache. If that library or the binary's ctime &

mtime haven't changed, then don't even try to prelink it. If things have

really changed, it will be picked up on the next run of "prelink -af".

Version-Release number of selected component (if applicable):

prelink-0.3.2-1

How reproducible:

Always

Steps to Reproduce:

1.Run prelink -a -f on a directory with shell scripts & other executables

that can not be prelinked.

2\. Strace "prelink -a -q", and look for the "reads".

3\. Examine strace's output, and you'll see all of the reads that take

place.

Actual Results: Shell script:

  open("/bin/unicode_stop", O_RDONLY|O_LARGEFILE) = 5

  read(5, "#!/bin/sh\n# stop u", 18)      = 18

  close(5)                                = 0

....

Static Binary:

open("/bin/ash.static", O_RDONLY|O_LARGEFILE) = 5

read(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0", 18) = 18

fcntl64(5, F_GETFL)                     = 0x8000  (flags

O_RDONLY|O_LARGEFILE)

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0)  = 16

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0)  = 16

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0\3\0\1\0\0\0\0\201\4"...,

52, 0) = 52

pread(5, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0\3\0\1\0\0\0\0\201\4"...,

52, 0) = 52

pread(5, "\1\0\0\0\0\0\0\0\0\200\4\10\0\200\4\10\320d\7\0\320d\7"...,

128, 52) = 128

pread(5, "\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0"...,

920, 488632) = 920

close(5)

Un-prelinkable executable:

lstat64("/usr/lib/mozilla-1.6/regchrome", {st_mode=S_IFREG|0755,

st_size=14444,

...}) = 0

open("/usr/lib/mozilla-1.6/regchrome", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\2\0", 18) = 18

fcntl64(6, F_GETFL)                     = 0x8000 (flags

O_RDONLY|O_LARGEFILE)

pread(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0", 16, 0) = 16

...

open("/usr/lib/mozilla-1.6/libldap50.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                = 0

lstat64("/usr/lib/mozilla-1.6/libgtkxtbin.so", {st_mode=S_IFREG|0755,

st_size=14268, ...}) = 0

open("/usr/lib/mozilla-1.6/libgtkxtbin.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                = 0

lstat64("/usr/lib/mozilla-1.6/libjsj.so", {st_mode=S_IFREG|0755,

st_size=96752,

...}) = 0

open("/usr/lib/mozilla-1.6/libjsj.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                = 0

lstat64("/usr/lib/mozilla-1.6/mozilla-xremote-client",

{st_mode=S_IFREG|0755, st_size=12896, ...}) = 0

lstat64("/usr/lib/mozilla-1.6/regxpcom", {st_mode=S_IFREG|0755,

st_size=55144, ...}) = 0

lstat64("/usr/lib/mozilla-1.6/libgkgfx.so", {st_mode=S_IFREG|0755,

st_size=143012, ...}) = 0

open("/usr/lib/mozilla-1.6/libgkgfx.so", O_RDONLY|O_LARGEFILE) = 6

read(6, "\177ELF\1\1\1\0\0\0\0\0\0\0\0\0\3\0", 18) = 18

close(6)                                = 0

...

Expected Results:  All of these should have been simple lstat checks

rather than actual reads of the executables.

Additional info:

</pre>

Even if the author or maintainer never replies, it is still a good idea to enter the problem in the bug-tracking database. The problem and possible solution will be recorded, and some enthusiastic programmer may come along and fix the <a name="iddle2825"></a><a name="iddle2826"></a><a name="iddle2827"></a><a name="iddle2828"></a><a name="iddle2829"></a>problem.