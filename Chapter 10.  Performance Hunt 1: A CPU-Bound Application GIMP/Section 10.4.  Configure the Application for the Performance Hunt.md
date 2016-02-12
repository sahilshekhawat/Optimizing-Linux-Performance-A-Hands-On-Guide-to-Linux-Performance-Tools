### 10.4\. Configure the Application for the Performance Hunt

The next step in <a name="iddle2322"></a><a name="iddle2323"></a><a name="iddle2324"></a><a name="iddle2325"></a>our investigation is to set up the application for the performance hunt by recompiling the application with symbols. Symbols allow the performance tools (such as <tt>oprofile</tt>) to investigate which functions and source lines are responsible for all the CPU time that is being spent.

For the GIMP, we download the latest GIMP tarball from its Web site, and then recompile it. In the case of GIMP and much open-source software, the first step in recompilation is running the <tt>configure</tt> command, which generates the makefiles that will be used to build the application. The <tt>configure</tt> command passes any flags present in the <tt>CFLAGS</tt> environmental variable into the makefile. In this case, because we want the GIMP to be built with symbols, we set the <tt>CFLAGS</tt> variable to contain <tt>-g3</tt>. This causes symbols to be included in the binaries that are built. This command is shown in [Listing 10.3](ch10lev1sec4.html#ch10ex03) and overrides the current value of the <tt>CFLAGS</tt> environmental variable and sets it to <tt>-g3</tt>.

<a name="ch10ex03"></a>

##### Listing 10.3\.

<pre>[root@localhost gimp-2.0.3]# env CFLAGS=-g3 ./configure

</pre>

We then make and install the version of GIMP with all the symbols included, and when we run this version, the performance tools will tell us where time is <a name="iddle2326"></a><a name="iddle2327"></a><a name="iddle2328"></a><a name="iddle2329"></a>being spent.