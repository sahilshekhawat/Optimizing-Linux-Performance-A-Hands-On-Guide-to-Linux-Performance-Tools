### 4.1\. Process Performance Statistics

The tools to analyze the performance of applications are varied and have existed in one form or another since the early days of UNIX. It is critical to understand how an application is interacting with the operating system, CPU, and memory system to understand its performance. Most applications are not self-contained and make many calls to the Linux kernel and different libraries. These calls to the Linux kernel (or system calls) may be as simple as "what's my PID?" or as complex as "read 12 blocks of data from the disk." Different systems calls will have different performance implications. Correspondingly, the library calls may be as simple as memory allocation or as complex as graphics window creation. These library calls may also have different performance characteristics.

<a name="ch04lev2sec1"></a>

#### 4.1.1\. Kernel Time Versus User Time

The most basic split of where an application may spend its time is between kernel and user time. Kernel time <a name="iddle0776"></a><a name="iddle0777"></a>is the time spent in the Linux kernel, and user time is the amount of time spent in application or library code. Linux has tools such <tt>time</tt> and <tt>ps</tt> that can indicate (appropriately enough) whether an application is spending its time in application or kernel code. It also has commands such as <tt>oprofile</tt> and <tt>strace</tt> that enable you to trace which kernel calls are made on the behalf of the process, as well as how long each of those calls took to complete.

<a name="ch04lev2sec2"></a>

#### 4.1.2\. Library Time Versus Application Time

Any application <a name="iddle0778"></a><a name="iddle0779"></a><a name="iddle0780"></a>with even a minor amount of complexity relies on system libraries to perform complex actions. These libraries may cause performance problems, so it is important to be able to see how much time an application spends in a particular library. Although it might not always be practical to modify the source code of the libraries directly to fix a problem, it may be possible to change the application code to call different or fewer library functions. The <tt>ltrace</tt> command and <tt>oprofile</tt> suite provide a way to analyze the performance of libraries when they are used by applications. Tools built in to the Linux loader, <tt>ld</tt>, helps you determine whether the use of many libraries slows down an <a name="iddle0781"></a><a name="iddle0782"></a><a name="iddle0783"></a>application's start time.

<a name="ch04lev2sec3"></a>

#### 4.1.3\. Subdividing Application Time

When the <a name="iddle0784"></a><a name="iddle0785"></a>application is known to be the bottleneck, Linux provides tools that enable you to profile an application to figure out where time is spent within an application. Tools such as <tt>gprof</tt> and <tt>oprofile</tt> can generate profiles of an application that pin down exactly which source line is causing large amounts of time to be spent.