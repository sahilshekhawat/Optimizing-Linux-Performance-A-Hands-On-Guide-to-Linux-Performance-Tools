### 11.6\. Run Application and Performance Tools

Next, we run <a name="iddle2509"></a><a name="iddle2510"></a><a name="iddle2511"></a><a name="iddle2512"></a><a name="iddle2513"></a><a name="iddle2514"></a>the application and take measurements using the performance tools. Because we already suspect that a complex interaction of many different processes and libraries might be the cause of the problem, we are going to start with <tt>oprofile</tt> and see what it has to say.

Because we only want <tt>oprofile</tt> to measure events that occur while we are opening the pop-up menus, we are going to use the command line shown in [Listing 11.3](ch11lev1sec6.html#ch11ex03) to start and stop the profiling immediately before and immediately after we run our script (named <tt>script.sh</tt>) that opens and closes 100 pop-up <a name="iddle2515"></a><a name="iddle2516"></a><a name="iddle2517"></a><a name="iddle2518"></a><a name="iddle2519"></a><a name="iddle2520"></a>menus.

<a name="ch11ex03"></a>

##### Listing 11.3\.

<pre>opcontrol —start ; ./script.sh ; opcontrol -stop

</pre>

Running <tt>opreport</tt> after that profiling information has been collected gives us the information shown in <a name="iddle2521"></a><a name="iddle2522"></a><a name="iddle2523"></a><a name="iddle2524"></a><a name="iddle2525"></a><a name="iddle2526"></a>[Listing 11.4](ch11lev1sec6.html#ch11ex04).

<a name="ch11ex04"></a>

##### Listing 11.4\.

<pre>CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

          TIMER:0|

  samples|      %|

------------------

     3134 27.1460 /usr/lib/libgobject-2.0.so.0.400.0

     1840 15.9376 /usr/lib/libglib-2.0.so.0.400.0

     1303 11.2863 /lib/tls/libc-2.3.3.so

     1048  9.0775 /lib/tls/libpthread-0.61.so

      900  7.7956 /usr/lib/libgtk-x11-2.0.so.0.400.0

      810  7.0160 /usr/X11R6/bin/Xorg

      719  6.2278 /usr/lib/libgdk-x11-2.0.so.0.400.0

      334  2.8930 /usr/lib/libpango-1.0.so.0.399.1

      308  2.6678 /lib/ld-2.3.3.so

      298  2.5812 /usr/X11R6/lib/libX11.so.6.2

      228  1.9749 /usr/lib/libbonoboui-2.so.0.0.0

      152  1.3166 /usr/X11R6/lib/libXft.so.2.1.2

</pre>

As you <a name="iddle2527"></a><a name="iddle2528"></a><a name="iddle2529"></a><a name="iddle2530"></a><a name="iddle2531"></a><a name="iddle2532"></a>can see, time is spent in many different libraries. Unfortunately, it is not at all clear which application is responsible for making those calls. In particular, we have no idea which processes have called the <tt>libgobject</tt> library. Fortunately, <tt>oprofile</tt> provides a way to record the shared libraries' functions that an application uses during a run. [Listing 11.5](ch11lev1sec6.html#ch11ex05) shows how to configure <tt>oprofile</tt>'s sample collection to separate the samples by library, which means that <tt>oprofile</tt> will attribute the samples collected in shared libraries to the programs that called them.

<a name="ch11ex05"></a>

##### Listing 11.5\.

<pre>opcontrol -p library; opcontrol ---reset

</pre>

After we rerun our test (using the commands in [Listing 11.3](ch11lev1sec6.html#ch11ex03)), <tt>opreport</tt> splits up the library samples per <a name="iddle2533"></a><a name="iddle2534"></a><a name="iddle2535"></a><a name="iddle2536"></a><a name="iddle2537"></a><a name="iddle2538"></a>application, as shown in [Listing 11.6](ch11lev1sec6.html#ch11ex06).

<a name="ch11ex06"></a>

##### Listing 11.6\.

<pre>[root@localhost menu_work]# opreport  -f

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

          TIMER:0|

  samples|      %|

------------------

     8172 61.1311 /usr/bin/nautilus

                  TIMER:0|

          samples|      %|

          ------------------

             3005 36.7719 /usr/lib/libgobject-2.0.so.0.400.0

             1577 19.2976 /usr/lib/libglib-2.0.so.0.400.0

              826 10.1077 /lib/tls/libpthread-0.61.so

              792  9.6916 /lib/tls/libc-2.3.3.so

              727  8.8962 /usr/lib/libgtk-x11-2.0.so.0.400.0

              391  4.7846 /usr/lib/libgdk-x11-2.0.so.0.400.0

              251  3.0715 /usr/lib/libpango-1.0.so.0.399.1

              209  2.5575 /usr/lib/libbonoboui-2.so.0.0.0

              140  1.7132 /usr/X11R6/lib/libX11.so.6.2

               75  0.9178 /usr/X11R6/lib/libXft.so.2.1.2

               54  0.6608 /usr/lib/libpangoxft-1.0.so.0.399.1

               23  0.2814 /usr/lib/libnautilus-private.so.2.0.0

               ....

</pre>

If we drill down into <a name="iddle2539"></a><a name="iddle2540"></a><a name="iddle2541"></a><a name="iddle2542"></a><a name="iddle2543"></a><a name="iddle2544"></a>the <tt>libgobject</tt> and <tt>libglib</tt> libraries, we can see exactly which functions are being called, as shown in [Listing 11.7](ch11lev1sec6.html#ch11ex07).

<a name="ch11ex07"></a>

##### Listing 11.7\.

<pre>[root@localhost menu_work]# opreport  -lf /usr/lib/libgobject-

2.0.so.0.400.0

...

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

samples  %        image name               app name

symbol name

394      11.7753  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

g_type_check_instance_is_a

248       7.4118  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

g_bsearch_array_lookup_fuzzy

208       6.2164  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

g_signal_emit_valist

162       4.8416  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

signal_key_cmp

147       4.3933  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

signal_emit_unlocked_R

137       4.0944  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

__i686.get_pc_thunk.bx

90        2.6898  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

g_type_value_table_peek

85        2.5403  /usr/lib/libgobject-2.0.so.0.400.0 /usr/bin/nautilus-

type_check_is_value_type_U

...

opreport  -lf /usr/lib/libglib-2.0.so.0.400.0

CPU: CPU with timer interrupt, speed 0 MHz (estimated)

Profiling through timer interrupt

samples  %        image name               app name

symbol name

385      18.0075  /usr/lib/libglib-2.0.so.0.400.0 /usr/bin/nautilus-

g_hash_table_lookup

95        4.4434  /usr/lib/libglib-2.0.so.0.400.0 /usr/bin/nautilus-

g_str_hash

78        3.6483  /usr/lib/libglib-2.0.so.0.400.0 /usr/bin/nautilus-

g_data_set_internal

78        3.6483  /usr/lib/libglib-2.0.so.0.400.0 /usr/bin/nautilus-

g_pattern_ph_match

70        3.2741  /usr/lib/libglib-2.0.so.0.400.0 /usr/bin/nautilus-

__i686.get_pc_thunk.bx

...

</pre>

From the <a name="iddle2545"></a><a name="iddle2546"></a><a name="iddle2547"></a><a name="iddle2548"></a><a name="iddle2549"></a><a name="iddle2550"></a><tt>oprofile</tt> output, we can see that nautilus spends a significant amount of time in the <tt>libgobject</tt> library and, in particular, in the <tt>g_type_check_instance_is_a</tt> function. However, it is unclear what function within the nautilus file manager called these functions. In fact, the functions may not even be called directly from nautilus, instead being made by other shared library calls that nautilus is making.

We next <a name="iddle2551"></a>use <tt>ltrace</tt>, the shared library tracer, to try to figure out which library calls are the most expensive and ultimately what is calling the <tt>g_type_check_instance_is_a</tt> function. Because we are concerned primarily about which functions nautilus is calling, rather than the exact timing information, it is only necessary to open a pop-up menu once rather than 100 times. Because <tt>ltrace</tt> will catch every single shared library call for a single run, if we create 100 pop-up menus, <tt>ltrace</tt> would just show the same profile information 100 times.

This procedure for capturing shared library usage information is similar to how we did it for the GIMP. We first start nautilus as normal. Then before we open up a pop-up menu, we attach to the nautilus process using the following <tt>ltrace</tt> command:

<pre>ltrace -c -p <pid_of_nautilus>.

</pre>

We right-click in the nautilus background to bring up the menu, and then immediately kill the <tt>ltrace</tt> process with a <Ctrl-C>. After tracing the pop-up, we get the summary table shown in <a name="iddle2552"></a><a name="iddle2553"></a><a name="iddle2554"></a><a name="iddle2555"></a><a name="iddle2556"></a><a name="iddle2557"></a>[Listing 11.8](ch11lev1sec6.html#ch11ex08).

<a name="ch11ex08"></a>

##### Listing 11.8\.

<pre>[ezolt@localhost menu_work]$ ltrace -c -p 2196

% time     seconds  usecs/call     calls      function

------ ----------- ----------- --------- --------------------

 32.75    0.109360      109360         1 bonobo_window_add_popup

 25.88    0.086414         257       335 g_cclosure_marshal_VOID__VOID

 14.98    0.050011         145       344 g_cclosure_marshal_VOID__OBJECT

  8.85    0.029546       29546         1 eel_pop_up_context_menu

  5.25    0.017540         604        29 gtk_widget_destroy

  5.22    0.017427        1340        13 g_cclosure_marshal_VOID__POINTER

  2.96    0.009888          41       241 g_free

  0.93    0.003101        3101         1 gtk_widget_get_ancestor

  0.45    0.001500        1500         1 gtk_widget_show

  0.45    0.001487         495         3 nautilus_icon_container_get_type

  0.43    0.001440          41        35 g_type_check_instance_cast

  0.38    0.001263        1263         1 nautilus_file_list_free

  0.34    0.001120        1120         1 gtk_widget_get_screen

  0.29    0.000978          46        21 gdk_x11_get_xatom_by_name

  0.25    0.000845          42        20 g_object_unref

  0.11    0.000358          89         4 g_type_check_class_cast

  0.09    0.000299          42         7 g_type_check_instance_is_a

  0.09    0.000285          40         7 g_cclosure_marshal_VOID__ENUM

  0.06    0.000187          37         5 strcmp

  0.04    0.000126         126         1 g_cclosure_marshal_VOID__STRING

  0.03    0.000093          93         1 gtk_menu_get_type

  0.03    0.000087          43         2 bonobo_window_get_type

  0.02    0.000082          82         1 nautilus_icon_container_get_selection

  0.02    0.000082          41         2 gtk_bin_get_type

  0.02    0.000081          40         2 gtk_widget_get_type

  0.02    0.000080          80         1 gtk_menu_set_screen

  0.02    0.000072          72         1 g_signal_connect_object

  0.02    0.000071          71         1 nautilus_file_set_boolean_metadata

  0.01    0.000041          41         1 nautilus_file_list_ref

  0.01    0.000040          40         1 eel_g_list_exactly_one_item

  0.01    0.000038          38         1 nautilus_icon_container_set_keep_aligned

------ ----------- ----------- --------- --------------------

100.00    0.333942                  1085 total

</pre>

We can see <a name="iddle2558"></a><a name="iddle2559"></a><a name="iddle2560"></a><a name="iddle2561"></a><a name="iddle2562"></a><a name="iddle2563"></a>something interesting in this table. <tt>ltrace</tt> shows a completely different function at the top of the list than <tt>oprofile</tt> did. This is mainly because <tt>oprofile</tt> and <tt>ltrace</tt> measure slightly different things. <tt>oprofile</tt> shows how much time is spent in actual functions, but none of the children. <tt>ltrace</tt> just shows how much time it takes for an external library call to complete. If that library function in turn calls other functions, <tt>ltrace</tt> does not record their individual timings. In fact, it currently does not even detect or display that these other library calls happened.

In this particular case, the function that <tt>oprofile</tt> says is the hottest function of <tt>libgobject</tt> (that is, <tt>g_type_check_instance_is_a</tt>) barely shows up on the <tt>ltrace</tt> profile at all. Even though this function is part of a shared library, the calls to it are not shown in the <tt>ltrace</tt> output. <tt>ltrace</tt> is not able to show the cross-library calls, and it is also not able to show calls that are made internally to the library. <tt>ltrace</tt> can only track when an external library or application calls into a shared library. When a library calls a function internally, <tt>ltrace</tt> cannot trace that the call has been made. In this case, all the functions that are prefixed with <tt>g_</tt> are actually part of the <tt>libgobject</tt> library. If any of them call <tt>g_type_check_instance_is_a</tt>, <tt>ltrace</tt> will not be able to detect it.

The most significant information that <tt>ltrace</tt> gives us is a set of a few library calls that our application makes that we can investigate. We can figure out where the library is being called, and possibly why all the time is being spent in <a name="iddle2564"></a><a name="iddle2565"></a><a name="iddle2566"></a><a name="iddle2567"></a><a name="iddle2568"></a><a name="iddle2569"></a>that library call.