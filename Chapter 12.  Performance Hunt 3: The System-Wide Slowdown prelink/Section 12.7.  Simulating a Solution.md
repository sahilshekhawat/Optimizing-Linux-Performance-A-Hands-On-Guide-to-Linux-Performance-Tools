### 12.7\. Simulating a Solution

The information <a name="iddle2779"></a><a name="iddle2780"></a><a name="iddle2781"></a><a name="iddle2782"></a><a name="iddle2783"></a><a name="iddle2784"></a><a name="iddle2785"></a>revealed by <tt>strace</tt> shows that <tt>prelink</tt> is spending a lot of time trying to open and analyze binaries that it cannot possibly prelink. The best way to test whether caching of nonprelinkable binaries could improve <tt>prelink</tt>'s performance is to modify <tt>prelink</tt> so that it adds all these unprelinkable binaries to its initial cache. Unfortunately, adding code to cache these "unprelinkable" binaries could be a complicated process that involves a good amount of knowledge about the internals of the <tt>prelink</tt> application. An easier method is to simulate the cache by replacing all the unprelinkable binaries with a known prelinkable binary. This causes all the formerly unprelinkable binaries to be ignored when quick mode is run. This is exactly what would happen if we had a working cache, so we can use it to estimate the performance increase we would see if <tt>prelink</tt> were able to cache and ignore unprelinkable binaries.

To start the experiment, we copy all the files in <tt>/usr/bin/</tt> to the <tt>sandbox</tt> directory and run <tt>prelink</tt> on this directory. This directory includes normal binaries, and shell scripts, and other libraries that cannot be prelinked. We then run <tt>prelink</tt> on the <tt>sandbox</tt> directory and tell it to create a new cache rather than rely on the system cache. This is shown in <a name="iddle2786"></a><a name="iddle2787"></a><a name="iddle2788"></a><a name="iddle2789"></a><a name="iddle2790"></a>[Listing 12.15](ch12lev1sec7.html#ch12ex15).

<a name="ch12ex15"></a>

##### Listing 12.15\.

<pre>/usr/sbin/prelink -C new_cache -f sandbox/

</pre>

Next, in [Listing 12.16](ch12lev1sec7.html#ch12ex16), we time how long it takes the quick mode of <tt>prelink</tt> to run. We had to run this multiple times until it gave a consistent result. (The first run warmed the cache for each of the succeeding runs.) The baseline time in [Listing 12.16](ch12lev1sec7.html#ch12ex16) is .983 seconds. We have to beat this time for our optimization (improving the cache) to be worth investigating.

<a name="ch12ex16"></a>

##### Listing 12.16\.

<pre>time /usr/sbin/prelink -C new_cache -q sandbox/

real    0m0.983s

user    0m0.597s

sys     0m0.386s

</pre>

Next, in <a name="iddle2791"></a><a name="iddle2792"></a><a name="iddle2793"></a><a name="iddle2794"></a><a name="iddle2795"></a><a name="iddle2796"></a>[Listing 12.17](ch12lev1sec7.html#ch12ex17), we run <tt>strace</tt> on this <tt>prelink</tt> command. This is to record which files <tt>prelink</tt> opens in the <tt>sandbox</tt> directory.

<a name="ch12ex17"></a>

##### Listing 12.17\.

<pre>strace -o strace_prelink_sandbox /usr/sbin/prelink -C new_cache -q

sandbox/

</pre>

Next we create a new directory, sandbox2, into which we once again copy all the binaries in the /usr/bin directory. However, we overwrite all the files that <tt>prelink</tt> "opened" in the preceding <tt>strace</tt> output with a known good binary, less, which can be prelinked. We copy the less on to all the problem binaries rather than just deleting them, so that both sandboxes contain the same number of files. After we set up the second sandbox, we run the full version of <tt>prelink</tt> on this new directory using the command in [Listing 12.18](ch12lev1sec7.html#ch12ex18).

<a name="ch12ex18"></a>

##### Listing 12.18\.

<pre>[root@localhost prelink]#/usr/sbin/prelink -C new_cache2 -f sandbox2/

</pre>

Finally, we <a name="iddle2797"></a><a name="iddle2798"></a><a name="iddle2799"></a><a name="iddle2800"></a><a name="iddle2801"></a><a name="iddle2802"></a>time the run of the quick mode and compare it to our baseline.

Again, we had to run it several times, where the first time warmed the cache. In [Listing 12.19](ch12lev1sec7.html#ch12ex19), we can see that we did, indeed, see a performance increase. The time to execute the <tt>prelink</tt> dropped from ~.98 second to ~.29 seconds.

<a name="ch12ex19"></a>

##### Listing 12.19\.

<pre>[root@localhost prelink]# time /usr/sbin/prelink -C new_cache2 -q

sandbox2/

real    0m0.292s

user    0m0.158s

sys     0m0.134s

</pre>

Next, we compare the <tt>strace</tt> output of the two different runs to verify that the number of reads did, in fact, decrease. [Listing 12.20](ch12lev1sec7.html#ch12ex20) shows the <tt>strace</tt> summary information from sandbox, which contained binaries that <tt>prelink</tt> could not link.

<a name="ch12ex20"></a>

##### Listing 12.20\.

<pre>execve("/usr/sbin/prelink", ["/usr/sbin/prelink", "-C", "new_cache",

"-q", "sandbox/"], [/* 20 vars */]) = 0

% time     seconds  usecs/call     calls    errors syscall

------ ----------- ----------- --------- --------- ----------------

 62.06    0.436563          48      9133           read

 13.87    0.097551          15      6504           lstat64

  6.20    0.043625          18      2363        10 stat64

  5.62    0.039543          21      1922           pread

  3.93    0.027671         374        74           vfork

  1.78    0.012515           9      1423           getcwd

  1.65    0.011594         644        18           getdents64

  1.35    0.009473          15       623         1 open

  0.90    0.006300           8       770           close

.....

100.00    0.703400                 24028        85 total

</pre>

[Listing 12.21](ch12lev1sec7.html#ch12ex21) shows <a name="iddle2803"></a><a name="iddle2804"></a><a name="iddle2805"></a><a name="iddle2806"></a><a name="iddle2807"></a><a name="iddle2808"></a>the <tt>strace</tt> summary from <tt>sandbox</tt> where <tt>prelink</tt> could link all the binaries.

<a name="ch12ex21"></a>

##### Listing 12.21\.

<pre>execve("/usr/sbin/prelink", ["/usr/sbin/prelink", "-C", "new_cache2",

"-q", "sandbox2/"], [/* 20 vars */]) = 0

% time     seconds  usecs/call     calls    errors syscall

------ ----------- ----------- --------- --------- ----------------

 54.29    0.088766          15      5795           lstat64

 26.53    0.043378          19      2259        10 stat64

  8.46    0.013833           8      1833           getcwd

  6.95    0.011363         631        18           getdents64

  2.50    0.004095        2048         2           write

  0.37    0.000611         611         1           rename

  0.26    0.000426          39        11         1 open

...

100.00    0.163515                  9973        11 total

</pre>

As you can see from the differences in [Listing 12.20](ch12lev1sec7.html#ch12ex20) and [Listing 12.21](ch12lev1sec7.html#ch12ex21), we have dramatically reduced the number of reads done in the directory. In addition, we have significantly reduced the amount of time required to <tt>prelink</tt> the directory. Caching and avoiding unprelinkable executables looks like a <a name="iddle2809"></a><a name="iddle2810"></a><a name="iddle2811"></a><a name="iddle2812"></a><a name="iddle2813"></a><a name="iddle2814"></a>promising optimization.