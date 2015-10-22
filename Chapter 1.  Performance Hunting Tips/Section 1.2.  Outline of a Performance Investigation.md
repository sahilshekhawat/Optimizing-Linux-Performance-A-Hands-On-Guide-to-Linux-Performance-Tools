### 1.2\. Outline of a Performance Investigation

This section outlines a series of essential steps as you begin a performance investigation. Because the ultimate goal is to fix the problem, the best idea is to research the problem before you even touch a performance tool. Following a particular protocol is an efficient way to solve your problem without wasting valuable time.

<a name="ch01lev2sec7"></a>

#### 1.2.1\. Finding a Metric, Baseline, and Target

The first step in a performance investigation is to determine the current performance and figure out how much it needs to be improved. If your system is significantly underperforming, you may decide that it is worth the time to investigate. However, if the system is performing close to its peak values, it might not be worth an investigation. Figuring out the peak performance values helps you to set reasonable performance expectations and gives you a performance goal, so that you know when to stop optimizing. You can always tweak the system just a little more, and with no performance target, you can waste a lot of time squeezing out that extra percent of performance, even though you may not actually need it.

<a name="ch01lev3sec1"></a>

##### 1.2.1.1 Establish a Metric

To figure out when <a name="iddle0035"></a><a name="iddle0036"></a>you have finished, you must create or use an already established metric of your system's performance. A metric is an objective measurement that indicates how the system is performing. For example, if you are optimizing a Web server, you could choose "serviced Web requests per second." If you do not have an objective way to measure the performance, it can be nearly impossible to determine whether you are making any progress as you tune the system.

<a name="ch01lev3sec2"></a>

##### 1.2.1.2 Establish a Baseline

After you figure <a name="iddle0037"></a><a name="iddle0038"></a>out how you are going to measure the performance of a particular system or application, it is important to determine your current performance levels. Run the application and record its performance before any tuning or optimization; this is called the baseline value, and it is the starting point for the performance investigation.

<a name="ch01lev3sec3"></a>

##### 1.2.1.3 Establish a Target

After you pick <a name="iddle0039"></a><a name="iddle0040"></a>a metric and baseline for the performance, it is important to pick a target. This target guides you to the end of the performance hunt. You can indefinitely tweak a system, and you can always get it just a little better with more and more time. If you pick your target, you will know when have finished. To pick a reasonable goal, the following are good starting points:

*   <span class="docEmphasis">Find others with a similar configuration and ask for their performance measurements</span>— This is an ideal situation. If you can find someone with a similar system that performs better, not only will you be able to pick a target for your system, you may also be able to work with that person to determine why your configuration is slower and how your configurations differ. Using another system as a reference can prove immensely useful when investigating a problem.

*   <span class="docEmphasis">Find results of industry standard benchmarks</span>— Many Web sites compare benchmark results of various aspects of computing systems. Some of the benchmark results can be achieved only with a heroic effort, so they might not represent realistic use. However, many benchmark sites have the configuration used for particular results. These configurations can provide clues to help you tune the system.

*   <span class="docEmphasis">Use your hardware with a different OS or application</span>— It may be possible to run a different application on your system with a similar function. For example, if you have two different Web servers, and one performs slowly, try a different one to see whether it performs any better. Alternatively, try running the same application on a different operating system. If the system performs better in either of these cases, you know that your original application has room for improvement.

If you use existing performance information to guide your target goal, you have a much better chance of picking a target that is aggressive but not <a name="iddle0041"></a><a name="iddle0042"></a>impossible to reach.

<a name="ch01sb02"></a>

<table cellspacing="0" width="90%" border="1" cellpadding="5">

<tbody>

<tr>

<td>

## Grabbing the Low-Hanging Fruit

Another approach to the performance hunt is pick a certain amount of time for the hunt and, instead of picking a target, optimize as much as possible within that time period. If an application has never been optimized for a given workload, it often has a few problems with relatively easy fixes. These easy fixes are called the "low-hanging fruit."

Why "low-hanging fruit"? An analogy to a performance investigation is to imagine that you were hungry and standing at the base of an apple tree. You would likely grab for the apple closest to the ground and easiest for you to reach. These low-hanging apples will satisfy your hunger just as well as the harder-to-reach apples farther up the tree; however, picking them requires much less work. Similarly, if you are optimizing an application in a limited amount of time, you might just try to fix the easiest and obvious problems (low-hanging fruit) rather than making some of the more difficult and fundamental changes.

</td>

</tr>

</tbody>

</table>

<a name="ch01lev2sec8"></a>

#### 1.2.2\. Track Down the Approximate Problem

Use the performance <a name="iddle0043"></a>tools to take a first cut at determining the cause of the problem. By taking an initial rough cut at the problem, you get a high-level idea of the problem. The goal of the rough cut is to gather enough information to pass along to the other users and developers of this program, so that they can provide advice and tips. It is vitally important to have a well-written explanation of what you think the problem might be and what tests led you to that conclusion.

<a name="ch01lev2sec9"></a>

#### 1.2.3\. See Whether the Problem Has Already Been Solved

Your next goal <a name="iddle0044"></a>should be to determine whether others have already solved the problem. A performance investigation can be a lengthy and time-consuming affair. If you can just reuse the work of others, you will be done before you start. Because your goal is simply to improve the performance of the system, the best way to solve a performance problem is to rely on what someone else has already done.

Although you must take specific advice regarding performance problems with a grain of salt, the advice can be enlightening, enabling you to see how others may have investigated a similar problem, how they tried to solve the problem, and whether they succeeded.

Here are a few different places to look for performance <a name="iddle0045"></a>advice:

*   <span class="docEmphasis">Search the Web for similar error messages/problems</span>— This is usually <a name="iddle0046"></a>my first line of investigation. Web searches often reveal lots of information about the application or the particular error condition that you are seeing. They can also lead to information about another user's attempt to optimize the systems, and possibly tips about what worked and what did not. A successful search can yield pages of information that directly applies to your performance problem. Searching with Google or Google groups is a particularly helpful way to find people with similar performance problems.

*   <span class="docEmphasis">Ask for help on the application mailing lists</span>— Most popular or publicly developed software has an e-mail list of people who use that software. This is a perfect place to find answers to performance questions. The readers and contributors are usually experienced at running the software and making it perform well. Search the archive of the mailing list, because someone may have asked about a similar problem. Subsequent replies to the original message might describe a solution. If they do not, send an e-mail to the person who originally wrote about the problem and ask whether he or she figured out how to resolve it. If that fails, or no one else had a similar problem, send an e-mail describing your problem to the list; if you are lucky, someone may have already solved your problem.

*   <span class="docEmphasis">Send an e-mail to the developer</span>— Most Linux <a name="iddle0047"></a>software includes the e-mail address of the developer somewhere in the documentation. If an Internet search and the mailing list fails, you can try to send an e-mail to the developer directly. Developers are usually very busy, so they might not have time to answer. However, they know the application better than anyone else. If you can provide the developer with a coherent analysis of the performance problem, and are willing to work with the developer, he or she might be able to help you. Although his idea of the cause of the performance problem might not be correct, the developer might point you in a fruitful direction.

*   <span class="docEmphasis">Talk to the in-house developers</span>— Finally, if <a name="iddle0048"></a>this is a product being developed in-house, you can call or e-mail the in-house developers. This is pretty much the same as contacting the external developers, but the in-house people might be able to devote more time to your problem or point you to an internal knowledge base.

By relying on the work of others, you might be able to solve your problem before you even begin to investigate. At the very least, you will most likely be able to find some promising avenues to investigate, so it is always best to see <a name="iddle0049"></a>what others have found.

<a name="ch01lev2sec10"></a>

#### 1.2.4\. The Case Begins (Start to Investigate)

Now that you have exhausted the possibility of someone else solving the problem, the performance investigation must begin. Later chapters describe the tools and methods in detail, but <a name="iddle0050"></a>here are a few tips to make things work better:

*   <span class="docEmphasis">Isolate the problem</span>— If at all possible, eliminate any extraneous programs or applications that are running on the system you are investigating. A heavily loaded system with many different running applications can skew the information gathered by the performance tools and ultimately lead you down false paths.

*   <span class="docEmphasis">Use system difference to find causes</span>— If you can find a similar system that performs well, it can be a powerful aid in debugging your problem. One of the problems of using performance tools is that you do not necessarily have a good way of knowing whether the results from a performance tool indicate a problem. If you have a good system and a bad one, you can run the same performance tool on both systems and compare the results. If the results differ, you might be able to determine the cause of the problem by figuring out how the systems differ.

*   <span class="docEmphasis">Change one thing at a time</span>— This very important. To really determine where the problem lies, you should only make one change at a time. This might be time-consuming and cause you to run many different tests, but it is really the only way to figure out whether you have solved the problem.

*   <span class="docEmphasis">Always remeasure after optimizing</span>— If you are tweaking a system, it is important to remeasure everything after you change something. When you start modifying the system configuration, all the performance information that you previously generated might not be valid anymore. Usually, as you solve a performance problem, others jump in to take its place. The new problems may be very different from the old problems, so you really have to rerun your performance tools to make sure you are investigating the right problem.

Following these tips can help you avoid false leads and help to determine the cause of a performance <a name="iddle0051"></a>problem.

<a name="ch01lev2sec11"></a>

#### 1.2.5\. Document, Document, Document

As mentioned <a name="iddle0052"></a><a name="iddle0053"></a>previously, it is really important to document what you are doing so that you can go back at a later date and review it. If you have hunted down the performance problem, you will have a big file of notes and URLs fresh in your mind. They may be a jumbled disorganized mess, but as of now, you understand what they mean and how they are organized. After you solve the problem, take some time to rewrite what you have discovered and why you think that it is true. Include performance results that you've measured and experiments that you've done. Although it might seem like a lot of work, it can be very valuable. After a few months, it is easy to forget all the tests that you have done, and if you do not write down your results, you may end up redoing it. If you write a report when the tests are fresh in your mind, you will not have to do the work again, and can instead just rely on what you have written <a name="iddle0054"></a><a name="iddle0055"></a>down.