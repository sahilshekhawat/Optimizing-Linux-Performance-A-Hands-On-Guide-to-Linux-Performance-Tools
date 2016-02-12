### 11.8\. Using gdb to Generate Call Traces

The two different tools for retrieving information about which functions our application was calling gave us different information about which functions were the hot functions. We theorized that the high-level functions that <tt>ltrace</tt> reported were calling the low-level function that <tt>operofile</tt> was reporting. It would be nice to have a performance tool that could show us exactly which functions were calling <tt>g_type_check_instance_is_a</tt> to verify this theory.

Although no Linux performance tool shows us exactly which functions are calling a particular function, <tt>gprof</tt> <a name="iddle2598"></a>should be able to present this callback information, but this requires recompiling the application and all the libraries that it relies on with the <tt>-pg</tt> flag to be effective. For nautilus, which relies on 72 shared libraries, this can be a daunting and infeasible task, so we have to look for another solution. Newer versions of <tt>oprofile</tt> can also provide this type of information, but because <tt>oprofile</tt> only samples periodically, it will still not be able to account for every call to any given function.

Fortunately, we can creatively use <tt>gdb</tt> <a name="iddle2599"></a>to extract <a name="iddle2600"></a><a name="iddle2601"></a>that information. Using <tt>gdb</tt> to trace the application greatly slows down the run; however, we do not really care whether the trace takes a long time. We are interested in finding the number of times that a particular function is called rather than the amount of time it is called, so it is acceptable for the run to take a long time. Luckily, the creation of the pop-up menu is in the millisecond range; even if it is 1,000 times slower with <tt>gdb</tt>, it still only takes about 15 minutes to extract the full trace. The value of the information outweighs our wait to retrieve it.

In particular, to find which functions are calling <tt>g_type_check_instance_is_a</tt>, we are going to use a few different features of <tt>gdb</tt>. First, we use <tt>gdb</tt>'s ability to set a breakpoint at that function. Then we use <tt>gdb</tt>'s ability to generate a backtrace with <tt>bt</tt> at that breakpoint. These two features are really all that we need to figure out which functions are calling this <tt>g_type_check_instance_is_a</tt>, but manually recording the information and continuing would be tedious. We would need to type <tt>bt ; cont</tt> after each time <tt>gdb</tt> breaks in the function.

To solve this, use another one of <tt>gdb</tt>'s features. <tt>gdb</tt> can execute a given set of commands when it hits a breakpoint. By using the <tt>command</tt> command, we can tell <tt>gdb</tt> to execute <tt>bt; cont</tt> every time it hits the breakpoint in our function. So now the backtrace displays automatically, and the application continues running every time it hits <tt>g_type_check_instance_is_a</tt>.

Now we have to isolate when the trace actually runs. We could just set up the breakpoint in <tt>g_type_check_instance_is_a</tt> at the start of the nautilus execution, and <tt>gdb</tt> would show tracing information when it is called by any function. Because we only care about those functions that are called when we are creating a pop-up menu, we want to limit that tracing to only when pop-ups are being created. To do this, we set another breakpoint at the beginning and end of the <tt>fm_directory_view_pop_up_background_context_menu</tt> function. When we reach the first breakpoint, we turn on the backtracing in <tt>g_type_check_instance_is_a</tt>; when we reach the second breakpoint, we exit the debugger. This limits the backtrace information to that which is generated when we are creating a pop-up menu. Finally, we want to be able to save this backtrace information for post-processing. We can use <tt>gdb</tt>'s ability to log its output to a file to save the information for later. The commands passed into <tt>gdb</tt> to extract this <a name="iddle2602"></a><a name="iddle2603"></a><a name="iddle2604"></a><a name="iddle2605"></a><a name="iddle2606"></a><a name="iddle2607"></a>information are shown in [Listing 11.12](ch11lev1sec8.html#ch11ex12).

<a name="ch11ex12"></a>

##### Listing 11.12\.

<pre># Prevent gdb from stopping after a screenful of output

set height 0

# Turn on output logging to a file (default: gdb.txt)

set logging on

# Turn off output to the screen

set logging redirect on

# Stop when a popup menu is about to be created

break fm-directory-view.c:5730

# Start the application

run

# When we've stopped at the preceding breakpoint, setup

# the breakpoint in g_type_check_instance_is_a

break g_type_check_instance_is_a

# When we reach the breakpoint, print a backtrace and exit

command

bt

cont

end

# break after the popup was created and exit gdb

break fm-directory-view.c:5769

command

quit

end

# continue running

cont

</pre>

When running <a name="iddle2608"></a><a name="iddle2609"></a><a name="iddle2610"></a><a name="iddle2611"></a><a name="iddle2612"></a><a name="iddle2613"></a>these <tt>gdb</tt> commands and opening a pop-up menu, <tt>gdb</tt> churns away for several minutes and creates a 33MB file containing all the backtrace information for functions that called the <tt>g_type_check_instance_is_a</tt> function. A sample of one is shown in [Listing 11.13](ch11lev1sec8.html#ch11ex13).

<a name="ch11ex13"></a>

##### Listing 11.13\.

<pre>Breakpoint 2, g_type_check_instance_is_a (type_instance=0x9d2b720,

iface_type=164410736) at gtype.c:31213121      if (!type_instance ||

!type_instance->g_class)

#1  0x08099f09 in fm_directory_view_pop_up_background_context_menu

(view=0x9d2b720, event=0x9ceb628)

    at fm-directory-view.c:5731

#2  0x080a2911 in icon_container_context_click_background_callback

(container=0x80c5a2b, event=0x9ceb628,

    icon_view=0x9d2b720) at fm-icon-view.c:2141

#3  0x00da32be in g_cclosure_marshal_VOID__POINTER (closure=0x9d37620,

return_value=0x0, n_param_values=2,

    param_values=0xfef67320, invocation_hint=0xfef67218,

marshal_data=0x0) at gmarshal.c:601

#4  0x00d8e160 in g_closure_invoke (closure=0x9d37620,

return_value=0x9d2b720, n_param_values=164804384,

    param_values=0x9d2b720, invocation_hint=0x9d2b720) at gclosure.c:437

#5  0x00da2195 in signal_emit_unlocked_R (node=0x9d33140, detail=0,

instance=0x9d35130, emission_return=0x0,

    instance_and_params=0xfef67320) at gsignal.c:2436

#6  0x00da1157 in g_signal_emit_valist (instance=0x9d35130, signal_id=0,

detail=0, var_args=0xfef674b0 "") at gsignal.c:2195

....

</pre>

Although <a name="iddle2614"></a><a name="iddle2615"></a><a name="iddle2616"></a><a name="iddle2617"></a><a name="iddle2618"></a><a name="iddle2619"></a>this information is very detailed, it is not exactly in an easy-to-digest format. It would be better if each backtrace were on a single line, with each function separated by arrows. It would also be nice to get rid of the backtrace information above the call to <tt>fm_directory_view_pop_up_background_context_menu</tt>, because we know that every one of the calls will have that same backtrace information. We can use the python program, <tt>slice.py</tt>, shown in [Listing 11.14](ch11lev1sec8.html#ch11ex14) to do exactly that. The program takes the verbose output file generated by <tt>gdb</tt> and creates a nicely formatted call trace of every function that called <tt>fm_directory_view_pop_up_background_context_menu</tt>.

<a name="ch11ex14"></a>

##### Listing 11.14\.

<pre>#!/usr/bin/python

import sys

import string

funcs = ""

stop_at = "fm_directory_view_pop_up_background_context_menu"

for  line  in sys.stdin:

    parsed = string.split(line)

    if (line[:1] == "#"):

        if (parsed[0] == "#0"):

            funcs = parsed[1]

        elif (parsed[3] == stop_at):

            print funcs

            funcs = ""

        else:

            funcs = parsed[3] + "->" + funcs

</pre>

When we run the <tt>gdb.txt</tt> file <a name="iddle2620"></a><a name="iddle2621"></a><a name="iddle2622"></a><a name="iddle2623"></a><a name="iddle2624"></a><a name="iddle2625"></a>into this python program using the command line shown in [Listing 11.15](ch11lev1sec8.html#ch11ex15), we have a more consolidated output, an example of which is shown in [Listing 11.16](ch11lev1sec8.html#ch11ex16).

<a name="ch11ex15"></a>

##### Listing 11.15\.

<pre>cat gdb.txt | ./slice.py > backtrace.txt

</pre>

<a name="ch11ex16"></a>

##### Listing 11.16\.

<pre>....

create_popup_menu->gtk_widget_show->g_object_notify->g_type_check_

instance_is_a

create_popup_menu->gtk_widget_show->g_object_notify->g_object_ref->g_

type_check_instance_is_a

create_popup_menu->gtk_widget_show->g_object_notify->g_object_

notify_queue_add->g_param_spec_get_redirect_target->g_type_check_

instance_is_a

create_popup_menu->gtk_widget_show->g_object_notify->g_object_notify_

queue_add->g_param_spec_get_redirect_target->g_type_check_instance_is_a

create_popup_menu->gtk_widget_show->g_object_notify->g_object_unref->g_

type_check_instance_is_a

create_popup_menu->gtk_widget_show->g_object_unref->g_type_check_

instance_is_a

...

</pre>

Because the output lines are long, they have been wrapped when displayed in this book; in the text file, however, there is one backtrace per line. Each line ends with the <tt>g_type_check_instance_is_a</tt> function. Because each backtrace spans only one line, we can extract information about the backtraces using some common Linux tools, such as <tt>wc</tt>, which we can use to count the number of lines in <a name="iddle2626"></a><a name="iddle2627"></a><a name="iddle2628"></a><a name="iddle2629"></a><a name="iddle2630"></a><a name="iddle2631"></a>a particular file.

First, let's look at how many calls have been made to the <tt>g_type_check_instance_is_a</tt> function. This is the same as the number of backtraces and, hence, the number of lines in the <tt>backtrace.txt</tt> file. [Listing 11.17](ch11lev1sec8.html#ch11ex17) shows the <tt>wc</tt> command being called on our pruned backtrace file. The first number indicates the number of lines in the file.

<a name="ch11ex17"></a>

##### Listing 11.17\.

<pre>[ezolt@localhost menu_work]$ wc backtrace.txt

   6848    6848 3605551 backtrace.txt

</pre>

As you can see, the function has been called 6,848 times just to create the pop-up menu. Next, let's see how many of those functions are made on behalf of <tt>bonobo_window_add_popup</tt>. This is shown in <a name="iddle2632"></a><a name="iddle2633"></a><a name="iddle2634"></a><a name="iddle2635"></a><a name="iddle2636"></a><a name="iddle2637"></a>[Listing 11.18](ch11lev1sec8.html#ch11ex18).

<a name="ch11ex18"></a>

##### Listing 11.18\.

<pre>[ezolt@localhost menu_work]$ grep bonobo_window_add_popup backtrace.txt | wc

   6670    6670 3558590

</pre>

<tt>bonobo_window_add_popup</tt> is responsible for 6,670 of the calls to our hot function. Looking at the <tt>backtrace.txt</tt> file reveals few of these are direct calls; most are made from other functions that it calls. From this, it appears as if the <tt>bonobo_window_add_popup</tt> is indeed responsible for much of the CPU time that is being spent. However, we still have to confirm that this is the case.