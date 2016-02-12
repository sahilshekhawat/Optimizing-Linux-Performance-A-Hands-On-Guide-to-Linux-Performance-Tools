## Chapter 11\. Performance Hunt 2: A Latency-Sensitive Application (nautilus)

This chapter contains an example of how to use the Linux performance tools to find and fix a performance problem in a latency-sensitive application.

After reading this chapter, you should be able to

*   Use <tt>ltrace</tt> and <tt>oprofile</tt> to figure out where latency is being generated in a latency-sensitive application.

*   Use <tt>gdb</tt> to generate a stack trace for each call to a "hot" function.

*   Use performance tools to determine where time is spent for an application that uses many different shared libraries.

*   Use this chapter as a template to find the cause of high latency in a latency-sensitive application.