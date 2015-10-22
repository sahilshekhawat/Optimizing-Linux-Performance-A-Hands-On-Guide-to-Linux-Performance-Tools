### 1.1\. General Tips

<a name="ch01lev2sec1"></a>

#### 1.1.1\. Take Copious Notes (Save Everything)

Probably <a name="iddle0001"></a><a name="iddle0002"></a>the <span class="docEmphasis">most</span> important thing that you can do when investigating a performance problem is to record every output that you see, every command that you execute, and every piece of information that you research. A well-organized set of notes allows you to test a theory about the cause of a performance problem by simply looking at your notes rather than rerunning tests. This saves a huge amount of time. Write it down to create a permanent record.

When starting a performance investigation, I usually create a directory for the investigation, open a new "Notes" file in GNU emacs, and start to record information about the system. I then store performance results in this directory and store interesting and related pieces of information in the Notes file. I suggest that you add the following to your performance investigation file and <a name="iddle0003"></a><a name="iddle0004"></a>directory:

*   <span class="docEmphasis">Record the hardware/software configuration</span>— This <a name="iddle0005"></a><a name="iddle0006"></a><a name="iddle0007"></a><a name="iddle0008"></a>involves recording information about the hardware configuration (amount of memory and type of CPU, network, and disk subsystem) as well as the software environment (the OS and software versions and the relevant configuration files). This information may seem easy to reproduce later, but when tracking down a problem, you may significantly change a system's configuration. Careful and meticulous notes can be used to figure out the system's configuration during a particular test.

    Example: Save the output of <tt>cat /proc/pci</tt>, <tt>dmesg</tt>, and <tt>uname -a</tt> for each test.

*   <span class="docEmphasis">Save and organize performance results</span>— It <a name="iddle0009"></a>can be valuable to review performance results a long time after you run them. Record the results of a test with the configuration of the system. This allows you to compare how different configurations affect the performance results. It would be possible just to rerun the test if needed, but usually testing a configuration is a time-consuming process. It is more efficient just to keep your notes well organized and avoid repeating work.

*   <span class="docEmphasis">Write down the command-line invocations</span>— As you run performance tools, you will often create complicated and complex command lines that measure the exact areas of the system that interest you. If you want to rerun a test, or run the same test on a different application, reproducing these command lines can be annoying and hard to do right on the first try. It is better just to record exactly what you typed. You can then reproduce the exact command line for a future test, and when reviewing past results, you can also see exactly what you measured. The Linux command <tt>script</tt> (described in detail in [Chapter 8](ch08.html#ch08), "Utility Tools: Performance Tool Helpers") or "cut and paste" from a terminal is a good way to do this.

*   <span class="docEmphasis">Record research information and URLs</span>— As <a name="iddle0010"></a><a name="iddle0011"></a>you investigate a performance problem, it is import to record relevant information you found on the Internet, through e-mail, or through personal interactions. If you find a Web site that seems relevant, cut and paste the text into your notes. (Web sites can disappear.) However, also save the URL, because you might need to review the page later or the page may point to information that becomes important later in an investigation.

As you collect and record all this information, you may wonder why it is worth the effort. Some information may seem useless or misleading now, but it might be useful in the future. (A good performance investigation is like a good detective show: Although the clues are confusing at first, everything becomes clear in the end.) Keep the <a name="iddle0012"></a><a name="iddle0013"></a>following in mind as you investigate a problem:

> <span class="docEmphasis">The implications of results may be fuzzy</span>— It is not always clear what a performance tool is telling you. Sometimes, you need more information to understand the implications of a particular result. At a later point, you might look back at seemingly useless test results in a new light. The old information may actually disprove or prove a particular theory about the nature of the performance problem.
> 
> <span class="docEmphasis">All information is useful information (which is why you save it)</span>— It might not be immediately clear why you save information about what tests you have run or the configuration of the system. It can prove immensely useful when you try to explain to a developer or manager why a system is performing poorly. By recording and organizing everything you have seen during your investigation, you have proof to support a particular theory and a large base of test results to prove or disprove other theories.
> 
> <span class="docEmphasis">Periodically reviewing your notes can provide new insights</span>— When you have a big pool of information about your performance problem, review it periodically. Taking a fresh look allows you to concentrate on the results, rather than the testing. When many test results are aggregated and reviewed at the same time, the cause of the problem may present itself. Looking back at the data you have collected allows you test theories without actually running any <a name="iddle0014"></a><a name="iddle0015"></a>tests.

Although it is inevitable that you will have to redo some work as you investigate a problem, the less time that you spend redoing old work, the more efficient you will be. If you take copious notes and have a method to record the information as you discover it, you can rely on the work that you have already done and avoid rerunning tests and redoing research. To save yourself time and frustration, keep reliable and consistent notes.

For example, if you investigate a performance problem and eventually determine the cause to be a piece of hardware (slow memory, slow CPU, and so on), you will probably want to test this theory by upgrading that slow hardware and rerunning the test. It often takes a while to get new hardware, and a large amount of time might pass before you can rerun your test. When you are finally able, you want to be able to run an identical test on the new and old hardware. If you have saved your old test invocations and your test results, you will know immediately how to configure the test for the new hardware, and will be able to compare the new results with the old results that you have stored.

<a name="ch01lev2sec2"></a>

#### 1.1.2\. Automate Redundant Tasks

As you start to <a name="iddle0016"></a>tweak the system to improve performance, it can become easy to make mistakes when typing complicated commands. Inadvertently using incorrect parameters or configurations can generate misleading performance information. It is a good idea to automate performance tool invocations and application tests:

> <span class="docEmphasis">Performance tool invocations</span>— Some <a name="iddle0017"></a><a name="iddle0018"></a>Linux performance tools require a fairly complicated command line. Do yourself a favor and store them in a shell script, or put the complete commands in a reference file that you can use to cut and paste. This saves you frustration, and gives you some certainty that the command line you use to invoke the tools is the correct one.
> 
> <span class="docEmphasis">Application tests</span>— Most applications <a name="iddle0019"></a><a name="iddle0020"></a>have complicated configurations either through a command line or a configuration file. You will often rerun the application you are testing many times. You save frustration if you script the invocation. Although typing a 30-character command might seem easy at first, after you have done it 10 times you will appreciate the automation.

If you automate as much as you can, you will reduce mistakes. Automation with scripting can save time and help to avoid misleading information caused by improper tool and test <a name="iddle0021"></a><a name="iddle0022"></a><a name="iddle0023"></a>invocations.

For example, if you are trying to monitor a system during a particular workload or length of time, you might not be present when the test finishes. It proves helpful to have a script that, after the test has completed, automatically collects, names, and saves all the generated performance data and places it automatically in a "Results" directory. After you have this piece of infrastructure in place, you can rerun your tests with different optimizations and tunings without worrying about whether the data will be saved. Instead, you can turn your full attention to figuring out the cause of the problem rather than managing test <a name="iddle0024"></a><a name="iddle0025"></a><a name="iddle0026"></a>results.

<a name="ch01lev2sec3"></a>

#### 1.1.3\. Choose Low-Overhead Tools If Possible

In general, the act of observing a system modifies its behavior. (For you physics buffs, this is known as the Heisenberg uncertainty principle.)

Specifically, when <a name="iddle0027"></a>using performance tools, they change the way that the system behaves. When you investigate a problem, you want to see how the application performs and must deal with the error introduced by performance tools. This is a necessary evil, but you must know that it exists and try to minimize it. Some performance tools provide a highly accurate view of the system, but use a high-overhead way of retrieving the information. Tools with a very high overhead change system behavior more than tools with lower overhead. If you only need a coarse view of the system, it is better to use the tools with lower overhead even though they are not as accurate.

For example, the tool <tt>ps</tt> can give you a pretty good, but coarse, overview of the quantity and type of memory that an application is using. More accurate but invasive tools, such as <tt>memprof</tt> or <tt>valgrind</tt>, also provide this information, but may change the behavior of the system by using more memory or CPU than the original application would <a name="iddle0028"></a>alone.

<a name="ch01lev2sec4"></a>

#### 1.1.4\. Use Multiple Tools to Understand the Problem

Although it would be <a name="iddle0029"></a>extraordinarily convenient if you needed only one tool to figure out the cause of a performance problem, this is rarely the case. Instead, each tool you use provides a hint of the problem's cause, and you must use several tools in concert to really understand what is happening. For example, one performance tool may tell you that the system has a high amount of disk I/O, and another tool may show that the system is using a large amount of swap. If you base your solution only on the results of the first tool, you may simply purchase a faster disk drive (and find that the performance problem has only improved slightly). Using the tools together, however, you determine that the high amount of disk I/O results from the high amount of swap that is being used. In this case, you might reduce the swapping by buying more memory (and thus cause the high disk I/O to disappear).

Using multiple performance tools together often gives you a much clearer picture of the performance problem than is possible with any single <a name="iddle0030"></a>tool.

<a name="ch01sb01"></a>

<table cellspacing="0" width="90%" border="1" cellpadding="5">

<tbody>

<tr>

<td>

## Parable of the Blind Men and the Elephant

Three blind men approach a mighty elephant to try to figure out what it is like. The first man pulls on the tail and says, "The elephant is like a rope." The second man touches the elephant's leg and says, "The elephant is like a tree." The third man touches the elephant's side and says, "The elephant is like a mighty wall."

Obviously, not one of them had the correct answer. If they had shared and combined their impressions, however, they might have discovered the truth about the elephant. Don't be like the blind men with the elephant. Use multiple performance tools together to verify the cause of a problem.

</td>

</tr>

</tbody>

</table>

<a name="ch01lev2sec5"></a>

#### 1.1.5\. Trust Your Tools

One of the most <a name="iddle0031"></a>exciting and frustrating times during a performance hunt is when a tool shows an "impossible" result. Something that "cannot" happen has clearly happened. The first instinct is to believe that the tools are broken. Do not be fooled. The tools are impartial. Although they can be incorrect, it is more likely that the application is doing what it should not be doing. Use the tools to investigate the problem.

For example, the Gnome calculator uses more than 2,000 system calls just to launch and then exit. Without the performance tools to prove this fact, it seems unlikely that this many system calls would be necessary to just start and stop an application. However, the performance tools can show where and why <a name="iddle0032"></a>it is happening.

<a name="ch01lev2sec6"></a>

#### 1.1.6\. Use the Experience of Others (Cautiously)

When <a name="iddle0033"></a>investigating any performance problem, you may find the task overwhelming. Do not go it alone. Ask the developers whether they have seen similar problems. Try to find someone else who has already solved the problem that you are experiencing. Search the Web for similar problems and, hopefully, solutions. Send e-mail to user lists and to developers.

This piece of advice comes with a word of warning: Even the developers who think that they know their applications are not always right. If the developer disagrees with the performance tool data, the developer might be wrong. Show developers your data and how you came to a particular conclusion. They will usually help you to reinterpret the data or fix the problem. Either way, you will be a little bit further along in your investigation. Do not be afraid to disagree with developers if your data shows something happening that should not be happening.

For example, you can often solve performance problems by following instructions you find from a Google search of similar problems. When investigating a Linux problem, many times, you will find that others have run into it before (even if it was years ago) and have reported a solution on a public mailing list. It is easy to use Google, and it can save you days of <a name="iddle0034"></a>work.