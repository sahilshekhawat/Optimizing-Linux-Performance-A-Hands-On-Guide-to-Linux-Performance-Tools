## Chapter 10\. Performance Hunt 1: A CPU-Bound Application (GIMP)

This chapter contains an example of how to use the Linux performance tools to find and fix performance problems in a CPU-bound application.

After reading this chapter, you should be able to

*   Figure out which source lines are using all the CPU in a CPU-bound application.

*   Use <tt>ltrace</tt> and <tt>oprofile</tt> to figure out how often an application is calling various internal and external functions.

*   Look for patterns in the applications source, and search online for information about how an application behaves and possible solutions.

*   Use this chapter as a template for tracking down a CPU-related performance problem.