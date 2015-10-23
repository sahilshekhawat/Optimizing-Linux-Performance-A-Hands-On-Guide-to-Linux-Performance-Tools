## Chapter 5\. Performance Tools: Process-Specific Memory

This chapter covers tools that enable you to diagnose an application's interaction with the memory subsystem as managed by the Linux kernel and the CPU. Because different layers of the memory subsystem have orders of magnitude differences in performance, fixing an application to efficiently use the memory subsystem can have a dramatic influence on an application's performance.

After reading this chapter, you should be able to

*   Determine how much memory an application is using (<tt>ps</tt>, <tt>/proc</tt>).

*   Determine which functions of an application are allocating memory (<tt>memprof</tt>).

*   Profile the memory usage of an application using both software simulation (<tt>kcachegrind</tt>, <tt>cachegrind</tt>) and hardware performance counters (<tt>oprofile</tt>).

*   Determine which processes are creating and using shared memory (<tt>ipcs</tt>).