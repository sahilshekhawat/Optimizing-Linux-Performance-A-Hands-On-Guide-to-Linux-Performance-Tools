## Chapter 4\. Performance Tools: Process-Specific CPU

After using the system-wide performance tools to figure out which process is slowing down the system, you must apply the process-specific performance tools to figure out how the process is behaving. Linux provides a rich set of tools to track the important statistics of a process and application's performance.

After reading this chapter, you should be able to

*   Determine whether an application's runtime is spent in the kernel or application.

*   Determine what library and system calls an application is making and how long they are taking.

*   Profile an application to figure out what source lines and functions are taking the longest time to complete.