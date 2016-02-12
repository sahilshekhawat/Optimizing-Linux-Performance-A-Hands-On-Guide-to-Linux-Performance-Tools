### 11.3\. Find a Baseline/Set a Goal

As with <a name="iddle2476"></a><a name="iddle2477"></a><a name="iddle2478"></a><a name="iddle2479"></a>the previous hunt, the first step is to determine the current state of the problem. To make our lives a little easier, and to avoid some of the profiling problems mentioned in the preceding section, we are going to cheat a little and make the pop-up menu problem look more similar to the long-running CPU-intensive tasks that we measured before. The amount of time that it takes for a single pop-up to appear is in the millisecond range, which makes it hard to accurately measure it with our performance profiling tools. As mentioned previously, it will be difficult to start them and stop them in the proper amount of time and guarantee that we are only measuring what we are interested in (that is, the CPU time spent to open up the actual menu). Here is where we cheat. Instead of opening up the menu just one time, we will open up the menu 100 times in rapid succession. This way, the total amount of time spent opening menus will increase by a factor of 100\. This enables us to use our profiling tools to capture information about how the menu is executing.

Because right-clicking 100 times would be tedious, and a human (unless very well trained) could not reliably open up a pop-up menu 100 times in a repeatable manner, we must automate it. To reliably open up the pop-up menu 100 times, we rely on the xautomation package. The xautomation package <a name="iddle2480"></a>is available at [http://hoopajoo.net/projects/xautomation.html](http://hoopajoo.net/projects/xautomation.html). It can send arbitrary X Window events to the X server, mimicking a user. After downloading the xautomation tar file, unzipping and compiling it, we can use it to automate the <a name="iddle2481"></a><a name="iddle2482"></a><a name="iddle2483"></a><a name="iddle2484"></a>right mouse click.

Unlike with the GIMP, we cannot simply measure the amount of CPU time used by nautilus to evaluate the time needed to create 100 pop-up menus. This is mainly because nautilus does not start immediately before a menu is opened and end immediately after. We are going to use wall-clock time to see how much time it takes to complete this task. This requires that the system not have any other things running while we run the test.

[Listing 11.1](ch11lev1sec3.html#ch11ex01) shows the shell script of xautomation commands that are used to open 100 pop-up menus in the nautilus file browser. When we run the test, we have to make sure that we have oriented the nautilus window so that none of the clicks actually opens a pop-up menu on a folder, and that instead all the pop-ups occur on the background. This is important because the code paths for the different pop-up menus could be radically different.

<a name="ch11ex01"></a>

##### Listing 11.1\.

<pre>#!/bin/bash

for i in 'seq 1 100';

do

      echo $i

      ./xte 'mousemove 100 100' 'mouseclick 3' 'mouseclick 3'

      ./xte 'mousemove 200 100' 'mouseclick 3' 'mouseclick 3'

done

</pre>

The <a name="iddle2485"></a><a name="iddle2486"></a><a name="iddle2487"></a><a name="iddle2488"></a>commands in [Listing 11.1](ch11lev1sec3.html#ch11ex01) move the cursor to position (100,100) on the X screen, and click the right mouse button (button 3). This brings up a menu. Then they click the right mouse button again, and this closes the menu. They then move to X position (100,100), and repeat the process.

Next, we use <tt>time</tt> to see how much the script of these 100 iterations takes to complete. This is our baseline time. When we do our optimizations, we will check them against this time to see whether they have improved. This baseline time for the stock Fedora 2 version of nautilus on my laptop is 26.5 seconds.

Finally, we have to pick a goal for our optimization path. One easy way to do this is to find an application that already has fast pop-up menus and see how long it takes for it to bring up a pop-up menu 100 times. A perfect example of this is xterm, which has nice snappy menus. Although the menus are not as complicated as those in nautilus, they should at least be considered an upper bound on how fast menus can be.

The pop-up menus on xterm work a little bit differently, so we have to slightly change the script to create 100 pop-ups. When xterm creates a pop-up, it requires that the left control key is depressed, so we have to slightly modify our automation script. This script is shown in [Listing 11.2](ch11lev1sec3.html#ch11ex02).

<a name="ch11ex02"></a>

##### Listing 11.2\.

<pre>#!/bin/bash

for i in 'seq 1 100';

do

   echo $i

  ./xte 'keydown Control_L' 'mousemove 100 100' 'mouseclick 3' 'mouseclick 3'

  ./xte 'keydown Control_L' 'mousemove 200 100' 'mouseclick 3' 'mouseclick 3' done

</pre>

When running xterm and timing the pop-up menu creation, xterm takes ~9.2 seconds to complete the script. nautilus has signficant (almost 17 seconds) room for improvement. It is probably unreasonable to expect the creation of nautilus's complex pop-up menus to be the same speed as those of xterm, so let's be conservative and set a goal of 10 percent, or 3 seconds. Hopefully, we will be able to do much better than this, or at least figure out why it is not possible to speed it <a name="iddle2489"></a><a name="iddle2490"></a><a name="iddle2491"></a><a name="iddle2492"></a>up any more.