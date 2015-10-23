### 3.1\. Memory Performance Statistics

Each system-wide Linux performance tool provides different ways to extract similar statistics. Although no tool displays all the statistics, some of the tools display the same statistics. The beginning of this chapter reviews the details of these statistics, and those descriptions are then referenced as the tools are described.

<a name="ch03lev2sec1"></a>

#### 3.1.1\. Memory Subsystem and Performance

In modern <a name="iddle0403"></a>processors, saving information to and retrieving information from the memory subsystem usually takes longer than the CPU executing code and manipulating that information. The CPU usually spends a significant amount of time idle, waiting for instructions and data to be retrieved from memory before it can execute them or operate based on them. Processors have various levels of cache that compensate for the slow memory performance. Tools such as <tt>oprofile</tt> can show where various processor cache misses can occur.

<a name="ch03lev2sec2"></a>

#### 3.1.2\. Memory Subsystem (Virtual Memory)

Any given Linux <a name="iddle0404"></a><a name="iddle0405"></a><a name="iddle0406"></a>system has a certain amount of RAM or physical memory. When addressing this physical memory, Linux breaks it up into chunks or "pages" of memory. When allocating or moving around memory, Linux operates on page-sized pieces rather than individual bytes. When reporting some memory statistics, the Linux kernel reports the number of pages per second, and this value can vary depending on the architecture it is running on. [Listing 3.1](ch03lev1sec1.html#ch03ex01) creates a small application that displays the number of bytes per page for the current architecture.

<a name="ch03ex01"></a>

##### Listing 3.1\.

<pre>#include <unistd.h>

int main(int argc, char *argv[])

{

  printf("System page size: %d\n",getpagesize());

}

</pre>

On the IA32 <a name="iddle0407"></a><a name="iddle0408"></a><a name="iddle0409"></a>architecture, the page size is 4KB. In rare cases, these page-sized chunks of memory can cause too much overhead to track, so the kernel manipulates memory in much bigger chunks, known as HugePages. These are on the order of 2048KB rather than 4KB and greatly reduce the overhead for managing very large amounts of memory. Certain applications, such as Oracle, use these huge pages to load an enormous amount of data in memory while minimizing the overhead that the Linux kernel needs to manage it. If HugePages are not completely filled with data, these can waste a significant amount of memory. A half-filled normal page wastes 2KB of memory, whereas a half-filled HugePage can waste 1,024KB of <a name="iddle0410"></a><a name="iddle0411"></a><a name="iddle0412"></a>memory.

The Linux kernel can take a scattered collection of these physical pages and present to applications a well laid-out <a name="iddle0413"></a><a name="iddle0414"></a>virtual memory space.

<a name="ch03lev3sec1"></a>

##### 3.1.2.1 Swap (Not Enough Physical Memory)

All systems have a <a name="iddle0415"></a><a name="iddle0416"></a><a name="iddle0417"></a>fixed amount of physical memory in the form of RAM chips. The Linux kernel allows applications to run even if they require more memory than available with the physical memory. The Linux kernel uses the hard drive as a temporary memory. This hard drive space is called swap space.

Although swap is an excellent way to allow processes to run, it is terribly slow. It can be up to 1,000 times slower for an application to use swap rather than physical memory. If a system is performing poorly, it usually proves helpful to determine how much swap the system is <a name="iddle0418"></a><a name="iddle0419"></a><a name="iddle0420"></a>using.

<a name="ch03lev3sec2"></a>

##### 3.1.2.2 Buffers and Cache (Too Much Physical Memory)

Alternatively, if your <a name="iddle0421"></a><a name="iddle0422"></a><a name="iddle0423"></a>system has much more physical memory than required by your applications, Linux will cache recently used files in physical memory so that subsequent accesses to that file do not require an access to the hard drive. This can greatly speed up applications that access the hard drive frequently, which, obviously, can prove especially useful for frequently launched applications. The first time the application is launched, it needs to be read from the disk; if the application remains in the cache, however, it needs to be read from the much quicker physical memory. This disk cache differs from the processor cache mentioned in the previous chapter. Other than <tt>oprofile</tt>, <tt>valgrind</tt>, and <tt>kcachegrind</tt>, most tools that report statistics about "cache" are actually referring to disk cache.

In addition to cache, Linux also uses extra <a name="iddle0424"></a><a name="iddle0425"></a><a name="iddle0426"></a>memory as buffers. To further optimize applications, Linux sets aside memory to use for data that needs to be written to disk. These set-asides are called buffers. If an application has to write something to the disk, which would usually take a long time, Linux lets the application continue immediately but saves the file data into a memory buffer. At some point in the future, the buffer is flushed to disk, but the application can continue immediately.

It can be discouraging to <a name="iddle0427"></a><a name="iddle0428"></a><a name="iddle0429"></a><a name="iddle0430"></a><a name="iddle0431"></a><a name="iddle0432"></a>see very little free memory in a system because of the cache and buffer usage, but this is not necessarily a bad thing. By default, Linux tries to use as much of your memory as possible. This is good. If Linux detects any free memory, it caches applications and data in the free memory to speed up future accesses. Because it is usually a few orders of magnitude faster to access things from memory rather than disk, this can dramatically improve overall performance. When the system needs the cache memory for more important things, the cache memory is erased and given to the system. Subsequent access to the object that <a name="iddle0433"></a><a name="iddle0434"></a><a name="iddle0435"></a><a name="iddle0436"></a><a name="iddle0437"></a><a name="iddle0438"></a>was previously cached has to go out to disk to be filled.

<a name="ch03lev3sec3"></a>

##### 3.1.2.3 Active Versus Inactive Memory

Active memory is <a name="iddle0439"></a><a name="iddle0440"></a><a name="iddle0441"></a><a name="iddle0442"></a>currently being used by a process. Inactive memory is memory that is allocated but has not been used for a while. Nothing is essentially different between the two types of memory. When required, the Linux kernel takes a process's least recently used memory pages and moves them from the active to the inactive list. When choosing which memory will be swapped to disk, the kernel chooses from the inactive memory list.

<a name="ch03lev3sec4"></a>

##### 3.1.2.4 High Versus Low Memory

For 32-bit <a name="iddle0443"></a><a name="iddle0444"></a><a name="iddle0445"></a><a name="iddle0446"></a>processors (for example, IA32) with 1GB or more of physical of memory, Linux must manage the physical memory as high and low memory. The high memory is not directly accessible by the Linux kernel and must be mapped into the low-memory range before it can be used. This is not a problem with 64-bit processors (such as AMD64/ EM6T, Alpha, or Itanium) because they can directly address additional memory that is available in current systems.

<a name="ch03lev3sec5"></a>

##### 3.1.2.5 Kernel Usage of Memory (Slabs)

In addition to <a name="iddle0447"></a><a name="iddle0448"></a><a name="iddle0449"></a><a name="iddle0450"></a>the memory that applications allocate, the Linux kernel consumes a certain amount for bookkeeping purposes. This bookkeeping includes, for example, keeping track of data arriving from network and disk I/O devices, as well as keeping track of which processes are running and which are sleeping. To manage this bookkeeping, the kernel has a series of caches that contains one or more slabs of memory. Each slab consists of a set of one or more objects. The amount of slab memory consumed by the kernel depends on which parts of the Linux kernel are being used, and can change as the type of load on the machine changes.