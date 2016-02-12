## Chapter 12\. Performance Hunt 3: The System-Wide Slowdown (prelink)

This chapter contains an example of how to use the Linux performance tools to find and fix a performance problem that affects the entire system rather than a specific application.

After reading this chapter, you should be able to

*   Track down which individual process is causing the system to slow down.

*   Use <tt>strace</tt> to investigate the performance behavior of a process that is not CPU-bound.

*   Use <tt>strace</tt> to investigate how an application is interacting with the Linux kernel.

*   Submit bug reports that describe a performance problem so that an author or maintainer has enough information to fix the problem.