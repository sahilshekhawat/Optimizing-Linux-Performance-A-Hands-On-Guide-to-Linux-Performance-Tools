### 10.3\. Find a Baseline/Set a Goal

This first step <a name="iddle2308"></a><a name="iddle2309"></a><a name="iddle2310"></a><a name="iddle2311"></a>in any performance hunt is to determine the current state of the problem. In the case of the GIMP filter, we need to figure out how much time it takes to run on a particular image. This is our baseline time. Once we have this baseline time, we can then try an optimization and see whether it decreases the execution time. Sometimes, it can be tricky to time how long something takes to execute. It is not as easy as using a stopwatch because the operating system may be scheduling other tasks at the same time that our particularly CPU-intensive job is running. In this case, if other jobs are running in addition to the CPU-intensive one, the amount of wall-clock time could be much greater than the amount of CPU time that the process actually uses. In this case, we are lucky; by looking at <tt>top</tt> as the filter is running, we can see that the <tt>lic</tt> process is taking up most of the CPU usage, as shown in [Listing 10.1](ch10lev1sec3.html#ch10ex01).

<a name="ch10ex01"></a>

##### Listing 10.1\.

<pre>[ezolt@localhost ktracer]$ top

top - 08:24:48 up 7 days,  9:08, 6 users,  load average: 1.04, 0.64, 0.76

  PID USER      PR  NI  VIRT  RES SHR S %CPU %MEM    TIME+  COMMAND

<span class="docEmphStrong">32744 ezolt     25   0 53696  45m 11m R 89.6 14.6   0:16.00 lic</span>

 2067 root      15   0 69252  21m 17m S  6.0  6.8 161:56.22 X

32738 ezolt     15   0 35292  27m 14m S  2.3  8.7   0:05.08 gimp

</pre>

From <a name="iddle2312"></a><a name="iddle2313"></a><a name="iddle2314"></a><a name="iddle2315"></a>this, we can deduce that GIMP actually spawns a separate process to run when running the filter. So when the filter is running, we can then use <tt>ps</tt> to track how much CPU time the process is using and when it has finished. When we have the PID of the filter using <tt>top</tt>, we can run the loop in [Listing 10.2](ch10lev1sec3.html#ch10ex02) and ask <tt>ps</tt> to periodically observe how much CPU time the filter is using.

<a name="ch10ex02"></a>

##### Listing 10.2\.

<pre>while true ; do sleep 1 ; ps  32744; done

  PID TTY      STAT   TIME COMMAND

32744 pts/0    R      <span class="docEmphStrong">2:46</span> /usr/local/lib/gimp/2.0/plug-ins/lic -gimp 8 6 -run 0

</pre>

<a name="ch10note01"></a>

<div class="docNote">

Note

If you need to time an application but do not have a stopwatch, you can use <tt>time</tt> and <tt>cat</tt> as a simple stopwatch. Just type <tt>time cat</tt> <a name="iddle2316"></a><a name="iddle2317"></a>when you want to start timing, and then press <Ctrl-D> when you are finished. <tt>time</tt> shows you how much time has passed.

</div>

When running the <tt>lic</tt> filter on the reference image (which is a fetching picture of my basement) and using the <tt>ps</tt> method just mentioned to time the filter, we can see from [Listing 10.2](ch10lev1sec3.html#ch10ex02) that it takes 2 minutes and 46 seconds to run on the entire image. This time is our baseline time. Now that we know the amount of time that the filter takes to run out of the box, we can set our goal for the performance hunt. It is not always clear how to set a reasonable goal for a performance investigation. A reasonable value for a goal can depend on several factors, including the amount of tuning that has already been done on the particular problem and the requirements of the user. It is often best to set the goal based on another quicker-performance application that does a similar thing. Unfortunately, we do not know of any GIMP filters that do similar work, so we have to make a guess. Because a 5 or 10 percent gain in performance is usually a reasonable goal for a relatively untuned piece of code, we'll set a goal of a 10 percent speedup, or a runtime of 2 minutes and 30 seconds.

Now that we have picked our goal, we need a way to guarantee that our performance optimizations are not unacceptably changing the results of the filter. In this case, we will run the original filter on the reference image and save the result into another file. We can then compare the output of our optimized filter to the output of the original filter and see whether the optimizations have changed <a name="iddle2318"></a><a name="iddle2319"></a><a name="iddle2320"></a><a name="iddle2321"></a>the output.