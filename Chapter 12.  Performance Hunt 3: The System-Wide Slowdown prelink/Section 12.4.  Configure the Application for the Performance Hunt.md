### 12.4\. Configure the Application for the Performance Hunt

The next step in <a name="iddle2710"></a><a name="iddle2711"></a><a name="iddle2712"></a><a name="iddle2713"></a>the investigation is to set up the application for the performance hunt. <tt>prelink</tt> is a small and self-contained application. In fact, it does not even use any shared libraries. (It is statically linked.) However, it is a good idea to recompile it with all the symbols so that we can examine it in the debugger (<tt>gdb</tt>) if we need to. Again, this tool uses the <tt>configure</tt> command to generate the makefiles. We must download the source to <tt>prelink</tt> and recompile it with symbols. We can once again download the source <tt>rpms</tt> for <tt>prelink</tt> from Red Hat. The source will be installed in <tt>/usr/src/redhat/SOURCES</tt>. Once we unpack <tt>prelink</tt>'s source code, we compile it as shown in <a name="iddle2714"></a><a name="iddle2715"></a><a name="iddle2716"></a><a name="iddle2717"></a>[Listing 12.6](ch12lev1sec4.html#ch12ex06).

<a name="ch12ex06"></a>

##### Listing 12.6\.

<pre>env CFLAGS=-g3 ./configure

gmake

</pre>

After <tt>prelink</tt> is configured and compiled, we can use the binary we compiled to investigate the performance problems.