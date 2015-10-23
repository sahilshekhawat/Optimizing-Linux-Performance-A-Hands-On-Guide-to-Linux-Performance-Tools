### 9.3\. Optimizing an Application

When optimizing an application, several areas of the application's execution may present a problem. This section directs you to the proper section based on the problem that you are seeing.

[Figure 9-1](ch09lev1sec3.html#ch09fig01) shows the steps that we will take to optimize the application.

<a name="ch09fig01"></a>

<center>

##### Figure 9-1\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/09fig01.gif)

</center>

To start diagnosing, go to [Section 9.3.1](ch09lev1sec3.html#ch09lev2sec1).

<a name="ch09lev2sec1"></a>

#### 9.3.1\. Is Memory Usage a Problem?

Use <tt>top</tt> or <tt>ps</tt> to determine <a name="iddle2163"></a><a name="iddle2164"></a>how much memory the application is using. If the application is consuming more memory than it should, go to [Section 9.6.6](ch09lev1sec6.html#ch09lev2sec27); otherwise, continue to [Section 9.3.2](ch09lev1sec3.html#ch09lev2sec2).

<a name="ch09lev2sec2"></a>

#### 9.3.2\. Is Startup Time a Problem?

If the amount <a name="iddle2165"></a><a name="iddle2166"></a>of time that the application takes to start up is a problem, go to [Section 9.3.3](ch09lev1sec3.html#ch09lev2sec3); otherwise, go to [Section 9.3.4](ch09lev1sec3.html#ch09lev2sec4).

<a name="ch09lev2sec3"></a>

#### 9.3.3\. Is the Loader Introducing a Delay?

To test whether the <a name="iddle2167"></a><a name="iddle2168"></a>loader is a problem, set the <tt>ld</tt> environmental variables described in the previous chapters. If the <tt>ld</tt> statistics show a significant delay when mapping all the symbols, try to reduce the number and size of libraries that the application is using, or try to prelink the binaries.

If the loader does appears to be the problem, go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9). If it does not, continue on to [Section 9.3.4](ch09lev1sec3.html#ch09lev2sec4).

<a name="ch09lev2sec4"></a>

#### 9.3.4\. Is CPU Usage (or Length of Time to Complete) a Problem?

Use <tt>top</tt> or <tt>ps</tt> to <a name="iddle2169"></a><a name="iddle2170"></a>determine the amount of CPU that the application uses. If the application is a heavy CPU user, or takes a particularly long time to complete, the application has a CPU usage problem.

Quite often, different parts of an application will have different performances. It may be necessary to isolate those parts that have poor performance so that their performance statistics are measured by the performance tools without measuring the statistics of those parts that do not have a negative performance impact. To facilitate this, it may be necessary to change an application's behavior to make it easier to profile. If a particular part of the application is performance-critical, when measuring the performance aspects of the total application, you would either try to measure <span class="docEmphasis">only</span> the performance statistics when the critical part is executing or make the performance-critical part run for such a long amount of time that the performance statistics from the uninteresting parts of the application are such a small part of the total performance statistics that they are irrelevant. Try to minimize the work that application is doing <tt>so</tt> that it only executes the performance-critical functions. For example, if we were collecting performance statistics from the entire run of an application, we would not want the startup and exit procedures to be a significant amount of the total time of the application runtime. In this case, it would be useful to start the application, run the time-consuming part many times, and then exit immediately. This allows the profilers (such as <tt>oprofile</tt> or <tt>gprof</tt>) to capture more information about slowly running code rather than parts that are executed but unrelated to the problem (such as launching and exiting). An even better solution is to change the application's source, so when the application is launched, the time-consuming portion is run automatically and then the program exits. This would help to minimize the profile data that does not pertain to the particular performance <a name="iddle2171"></a><a name="iddle2172"></a>problem.

If the application's CPU usage is a problem, skip to [Section 9.5](ch09lev1sec5.html#ch09lev1sec5). If it is not a problem, go to [Section 9.3.5](ch09lev1sec3.html#ch09lev2sec5).

<a name="ch09lev2sec5"></a>

#### 9.3.5\. Is the Application's Disk Usage a Problem?

If the application <a name="iddle2173"></a><a name="iddle2174"></a>is known to cause <a name="iddle2175"></a>an unacceptable amount of disk I/O, go to [Section 9.7.3](ch09lev1sec7.html#ch09lev2sec34) to determine what files it is accessing. If not, go to [Section 9.3.6](ch09lev1sec3.html#ch09lev2sec6).

<a name="ch09lev2sec6"></a>

#### 9.3.6\. Is the Application's Network Usage a Problem?

If the application <a name="iddle2176"></a><a name="iddle2177"></a><a name="iddle2178"></a>is known to cause an unacceptable amount of network I/O, go to [Section 9.8.6](ch09lev1sec8.html#ch09lev2sec40).

Otherwise, you have encountered an application performance issue that is not covered in this book. Go to [Section 9.9](ch09lev1sec9.html#ch09lev1sec9).