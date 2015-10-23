### 10.7\. Analyze the Results

Now that <a name="iddle2355"></a><a name="iddle2356"></a><a name="iddle2357"></a><a name="iddle2358"></a><a name="iddle2359"></a><a name="iddle2360"></a>we have used <tt>oprofile</tt> to collect information about where time is spent when the filter is running, we have to analyze the results to look for ways to change its execution and increase performance.

First, we use <tt>oprofile</tt> to look at how the entire system was spending time. This is shown in [Listing 10.6](ch10lev1sec7.html#ch10ex06).

<a name="ch10ex06"></a>

##### Listing 10.6\.

<pre>[root@localhost ezolt]# opreport -f | less

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

          TIMER:0|

  samples|      %|

------------------

    69896 36.9285 /usr/local/lib/libgimp-2.0.so.0.0.3

    44237 23.3719 /usr/local/lib/libgimpcolor-2.0.so.0.0.3

    28386 14.9973 /usr/local/lib/gimp/2.0/plug-ins/lic

    16133  8.5236 /usr/lib/libglib-2.0.so.0.400.0

....

</pre>

As [Listing 10.6](ch10lev1sec7.html#ch10ex06) shows, 75 <a name="iddle2361"></a><a name="iddle2362"></a><a name="iddle2363"></a><a name="iddle2364"></a><a name="iddle2365"></a><a name="iddle2366"></a>percent of the CPU time was spent in the <tt>lic</tt> process or GIMP-related libraries. Most likely, these libraries are called by the <tt>lic</tt> process, a fact that we can confirm by combining the information <a name="iddle2367"></a>that <tt>ltrace</tt> gives us with the information from <tt>oprofile</tt>. [Listing 10.7](ch10lev1sec7.html#ch10ex07) shows the library calls made for a small portion of the run of the filter.

<a name="ch10ex07"></a>

##### Listing 10.7\.

<pre>[ezolt@localhost ktracer]$ ltrace -p 32744 -c

% time     seconds  usecs/call     calls      function

------ ----------- ----------- --------- --------------------

 46.13  101.947798         272    374307 rint

 15.72   34.745099         278    124862 g_rand_double_range

 14.77   32.645236         261    124862 gimp_pixel_rgn_get_pixel

 13.01   28.743856         230    124862 gimp_rgba_set_uchar

 10.36   22.905472         183    124862 gimp_rgb_to_hsl

  0.00    0.006832        6832         1 gtk_widget_destroy

  0.00    0.003976        3976         1 gimp_progress_init

  0.00    0.003631        3631         1 g_rand_new

  0.00    0.001992        1992         1 gimp_drawable_get

  0.00    0.001802        1802         1 gimp_drawable_mask_bounds

  0.00    0.000184         184         1 g_malloc

  0.00    0.000118         118         1 gettext

  0.00    0.000100         100         1 gimp_pixel_rgn_init

------ ----------- ----------- --------- --------------------

100.00  221.006096                873763 total

</pre>

Next, we investigate <a name="iddle2368"></a><a name="iddle2369"></a><a name="iddle2370"></a><a name="iddle2371"></a><a name="iddle2372"></a><a name="iddle2373"></a><a name="iddle2374"></a>the information that <tt>oprofile</tt> gives us about where CPU time is being spent in each of the libraries, and see whether the hot functions in the libraries are the same as those that the filter calls. For each of the three top CPU-using images, we ask <tt>opreport</tt> to give us more details about which functions in the library are spending all the time. The results are shown in [Listing 10.8](ch10lev1sec7.html#ch10ex08) for the <tt>libgimp, libgimp-color</tt> libraries, and the <tt>lic</tt> process.

<a name="ch10ex08"></a>

##### Listing 10.8\.

<pre>[/tmp]# opreport -lf /usr/local/lib/libgimp-2.0.so.0.0.3

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

samples  %         symbol name

27136    38.8234   gimp pixel_rgn_get_pixel

14381    20.5749   gimp drawable_get_tile2

6571      9.4011   gimp tile_unref

6384      9.1336   gimp drawable_get_tile

3921      5.6098   gimp tile_cache_insert

3322      4.7528   gimp tile_ref

3057      4.3736   anonymous symbol from section .plt

2732      3.9087   gimp tile_width

1998      2.8585   gimp tile_height

...

[/tmp]# opreport -lf /usr/local/lib/libgimpcolor-2.0.so.0.0.3

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

samples  %         symbol name

31475    71.1508   gimp rgba_set_uchar

6251     14.1307   gimp bilinear_rgb

2941      6.6483   gimp rgb_multiply

2394      5.4118   gimp rgb_add

466       1.0534   gimp rgba_get_uchar

323       0.7302   gimp rgb_to_hsl

....

[/tmp]# opreport -lf /usr/local/lib/gimp/2.0/plug-ins/lic

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

samples  %         symbol name

11585    40.8124   getpixel

5185     18.2660   lic_image

4759     16.7653   peek

3287     11.5797   filter

1698      5.9818   peekmap

1066      3.7554   anonymous symbol from section .plt

316       1.1132   compute_lic

232       0.8173   rgb_to_hsl

111       0.3910   grady

106       0.3734   gradx

41        0.1444   poke

....

</pre>

As you can see by <a name="iddle2375"></a><a name="iddle2376"></a><a name="iddle2377"></a><a name="iddle2378"></a><a name="iddle2379"></a><a name="iddle2380"></a><a name="iddle2381"></a>comparing the output of <tt>ltrace</tt> in [Listing 10.8](ch10lev1sec7.html#ch10ex08), and the <tt>oprofile</tt> output in [Listing 10.9](ch10lev1sec7.html#ch10ex09), the <tt>lic</tt> filter is repeatedly calling the library functions that are spending all the time.

Next, we investigate the source code of the <tt>lic</tt> filter to determine how it is structured, what exactly its hot functions are doing, and how the filter calls the GIMP library functions. The <tt>lic</tt> function that <a name="iddle2382"></a><a name="iddle2383"></a><a name="iddle2384"></a><a name="iddle2385"></a><a name="iddle2386"></a><a name="iddle2387"></a>generated the most samples is the <tt>getpixel</tt> function, <a name="iddle2388"></a>shown by the <tt>opannotate</tt> output in [Listing 10.9](ch10lev1sec7.html#ch10ex09). <tt>opannotate</tt> shows the number of samples, followed by the total percentage of samples in a column to the left of the source. This enables you to look through the source and see which exact source lines are hot.

<a name="ch10ex09"></a>

##### Listing 10.9\.

<pre>opannotate --source /usr/local/lib/gimp/2.0/plug-ins/lic

....

               :static void

               :getpixel (GimpPixelRgn *src_rgn,

               :          GimpRGB      *p,

               :          gdouble       u,

               :          gdouble       v)

   428 1.5961  :{ /* getpixel total: 11198 41.7587 */

               :  register gint x1, y1, x2, y2;

               :  gint width, height;

               :  static GimpRGB pp[4];

               :

    98 0.3655  :  width = src_rgn->w;

    72 0.2685  :  height = src_rgn->h;

               :

  1148 4.2810  :  x1 = (gint)u;

  1298 4.8404  :  y1 = (gint)v;

               :

   603 2.2487  :  if (x1 < 0)

     1 0.0037  :    x1 = width - (-x1 % width);

               :  else

  1605 5.9852  :    x1 = x1 % width;

               :

    87 0.3244  :  if (y1 < 0)

               :    y1 = height - (-y1 % height);

               :  else

  1264 4.7136  :    y1 = y1 % height;

               :

  1358 5.0641  :  x2 = (x1 + 1) % width;

  1379 5.1425  :  y2 = (y1 + 1) % height;

               :

   320 1.1933  :  peek (src_rgn, x1, y1, &pp[0]);

   267 0.9957  :  peek (src_rgn, x2, y1, &pp[1]);

   285 1.0628  :  peek (src_rgn, x1, y2, &pp[2]);

   244 0.9099  :  peek (src_rgn, x2, y2, &pp[3]);

               :

   706 2.6328  :  *p = gimp_bilinear_rgb (u, v, pp);

    35 0.1305  :}

...

</pre>

There are a <a name="iddle2389"></a><a name="iddle2390"></a><a name="iddle2391"></a><a name="iddle2392"></a><a name="iddle2393"></a><a name="iddle2394"></a><a name="iddle2395"></a><a name="iddle2396"></a>few interesting things to note about the <tt>get_pixel</tt> function. First, it calls the <tt>gimp_bilinear_rgb</tt> function, which is one of the hot functions in the GIMP libraries. Second, it calls the <tt>peek</tt> function four times. If the <tt>get_pixel</tt> call is executed many times, the <tt>peek</tt> function <a name="iddle2397"></a>is executed four times as much. Using <tt>opannotate</tt> to look at the <tt>peek</tt> function (shown in [Listing 10.10](ch10lev1sec7.html#ch10ex10)), we can see that it calls <tt>gimp_pixel_rgn_get_pixel</tt> <a name="iddle2398"></a>and <tt>gimp_rgba_set_uchar</tt>, <a name="iddle2399"></a>which are top functions for <tt>libgimp</tt> and <tt>libgimp-color</tt> respectively.

<a name="ch10ex10"></a>

##### Listing 10.10\.

<pre>              :static void

                :peek (GimpPixelRgn *src_rgn,

                :      gint          x,

                :      gint          y,

                :      GimpRGB      *color)

   481  1.7937  :{ /* peek total:   4485 16.7251 */

                :  static guchar data[4] = { 0, };

                :

  1373  5.1201  :  gimp_pixel_rgn_get_pixel (src_rgn, data, x, y);

  2458  9.1662  :  gimp_rgba_set_uchar (color, data[0], data[1], data[2],

data[3]);

   173  0.6451  :}

</pre>

Although it is not quite clear exactly what the filter is <a name="iddle2400"></a><a name="iddle2401"></a><a name="iddle2402"></a><a name="iddle2403"></a><a name="iddle2404"></a>doing or what the library calls are used for, there are a few curious points. First, <tt>peek</tt> sounds like a function that would retrieve pixels from the image so that the filter can process them. We can check this hunch shortly. Second, most of the time spent in the filter does not appear to be spent running a mathematical algorithm on the image data. Instead of spending all the CPU time running calculations based on the values of the pixels, this filter appears to spend most of the time retrieving pixels to be manipulated. If this is really the case, perhaps it can be fixed.