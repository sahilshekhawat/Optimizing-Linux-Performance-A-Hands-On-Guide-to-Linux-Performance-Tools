## Chapter 6\. Performance Tools: Disk I/O

This chapter covers performance tools that help you gauge disk I/O subsystem usage. These tools can show which disks or partitions are being used, how much I/O each disk is processing, and how long I/O requests issued to these disks are waiting to be processed.

After reading this chapter, you should be able to

*   Determine the amount of total amount and type (read/write) of disk I/O on a system (<tt>vmstat</tt>).

*   Determine which devices are servicing most of the disk I/O (<tt>vmstat</tt>, <tt>iostat</tt>, <tt>sar</tt>).

*   Determine how effectively a particular disk is fielding I/O requests (<tt>iostat</tt>).

*   Determine which processes are using a given set of files (<tt>lsof</tt>).