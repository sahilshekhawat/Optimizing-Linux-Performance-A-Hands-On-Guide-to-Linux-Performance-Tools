### 10.6\. Run Application and Performance Tools

Next, we run the application and take measurements using the performance tools. Because the <tt>lic</tt> filter is called directly from the GIMP, we have to use tools that can attach and monitor an already running process.

In the case <a name="iddle2337"></a><a name="iddle2338"></a><a name="iddle2339"></a><a name="iddle2340"></a><a name="iddle2341"></a><a name="iddle2342"></a>of <tt>oprofile</tt>, we can start <tt>oprofile</tt>, run the filter, and then stop <tt>oprofile</tt> after the filter has been completed. Because the <tt>lic</tt> filter takes up approximately 90 percent of the CPU when running, the system-wide samples that <tt>oprofile</tt> collects will be mainly relevant for the <tt>lic</tt> filter. When <tt>lic</tt> starts to run, we start <tt>oprofile</tt> in another window; when <tt>lic</tt> finishes in that other window, we stop <tt>oprofile</tt>. The starting and stopping of <tt>oprofile</tt> is shown in [Listing 10.4](ch10lev1sec6.html#ch10ex04).

<a name="ch10ex04"></a>

##### Listing 10.4\.

<pre>[root@localhost ezolt]# opcontrol --start

Profiler running.

[root@localhost ezolt]# opcontrol --dump

[root@localhost ezolt]# opcontrol --stop

Stopping profiling.

</pre>

<tt>ltrace</tt> must be run a little differently. After the filter has been started, <tt>ltrace</tt> can be attached to the running process. Unlike <tt>oprofile</tt>, attaching <a name="iddle2343"></a><a name="iddle2344"></a><a name="iddle2345"></a><a name="iddle2346"></a><a name="iddle2347"></a><a name="iddle2348"></a><tt>ltrace</tt> to a process brings the entire process to a crawl. This can inaccurately inflate the amount of time taken for each library call; however, it provides information about the number of times each call is made. [Listing 10.5](ch10lev1sec6.html#ch10ex05) shows a listing from <tt>ltrace</tt>.

<a name="ch10ex05"></a>

##### Listing 10.5\.

<pre>[ezolt@localhost ktracer]$ ltrace -p 32744 -c

% time     seconds  usecs/call     calls       function

------ ----------- ----------- --------- --------------------

 43.61  156.419150         254    614050 rint

 16.04   57.522749         281    204684 gimp_rgb_to_hsl

 14.92   53.513609         261    204684 g_rand_double_range

 13.88   49.793988         243    204684 gimp_rgba_set_uchar

 11.55   41.426779         202    204684 gimp_pixel_rgn_get_pixel

  0.00    0.006287        6287         1 gtk_widget_destroy

  0.00    0.003702        3702         1 g_rand_new

  0.00    0.003633        3633         1 gimp_progress_init

  0.00    0.001915        1915         1 gimp_drawable_get

  0.00    0.001271        1271         1 gimp_drawable_mask_bounds

  0.00    0.000208         208         1 g_malloc

  0.00    0.000110         110         1 gettext

  0.00    0.000096          96         1 gimp_pixel_rgn_init

------ ----------- ----------- --------- --------------------

100.00  358.693497               1432794 total

</pre>

To get the full number of library calls, it is possible to let <tt>ltrace</tt> run until completion; however, it takes a really long time, so in this case, we pressed <Ctrl-C> after a long period of time had elapsed. This will not always work, because an application may go through different stages of execution, and if you stop it early, you may not have a complete picture of what functions the application is calling. However, this short sample will at least give us a starting point for <a name="iddle2349"></a><a name="iddle2350"></a><a name="iddle2351"></a><a name="iddle2352"></a><a name="iddle2353"></a><a name="iddle2354"></a>analysis.