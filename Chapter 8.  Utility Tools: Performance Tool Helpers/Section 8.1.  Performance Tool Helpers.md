### 8.1\. Performance Tool Helpers

Linux has a rich heritage of tools that can be used together and become greater than the sum of the parts. Performance tools are no different. Although performance tools are useful on their own, combining them with other Linux tools can significantly boost their effectiveness and ease of use.

<a name="ch08lev2sec1"></a>

#### 8.1.1\. Automating and Recording Commands

As mentioned in <a name="iddle1911"></a><a name="iddle1912"></a><a name="iddle1913"></a><a name="iddle1914"></a>an earlier <a name="iddle1915"></a><a name="iddle1916"></a><a name="iddle1917"></a><a name="iddle1918"></a>chapter, one of the most valuable steps in a performance investigation is to save the commands that are issued and results that are generated during a performance investigation. This allows you to review them later and look for new insights. To help with this, Linux provides the <tt>tee</tt> command, which enables you to save tool output to a file, and the <tt>script</tt> command, which records every key press and every output displayed on the screen. This information can be saved and reviewed later or used to create a script to automate test execution.

It is important to automate commands because it reduces the chance of errors and enables you to think about the problem without having to remember all the details. Both <a name="iddle1919"></a><a name="iddle1920"></a><a name="iddle1921"></a><a name="iddle1922"></a><a name="iddle1923"></a><a name="iddle1924"></a><a name="iddle1925"></a><a name="iddle1926"></a>the <tt>bash</tt> shell and the <tt>watch</tt> command enable you to periodically and automatically execute long and complicated command lines after typing them once. After you have the command line correct, <tt>bash</tt> and <tt>watch</tt> can periodically execute the command without the need to retype it.

<a name="ch08lev2sec2"></a>

#### 8.1.2\. Graphing and Analyzing Performance Statistics

In addition to <a name="iddle1927"></a><a name="iddle1928"></a><a name="iddle1929"></a><a name="iddle1930"></a>the tools for recording and automation, Linux provides powerful analysis tools that can help you understand the implications of performance statistics. Whereas most performance tools generate performance statistics as text output, it is not always easy to see patterns and trends over time. Linux provides the powerful <tt>gnumeric</tt> spreadsheet, which can import, analyze, and graph performance data. When you graph the data, the cause of a performance problem may become apparent, or it may at least open up new areas of investigation.

<a name="ch08lev2sec3"></a>

#### 8.1.3\. Investigating the Libraries That an Application Uses

Linux also <a name="iddle1931"></a><a name="iddle1932"></a><a name="iddle1933"></a><a name="iddle1934"></a><a name="iddle1935"></a>provides tools that enable you to determine which libraries an application relies on, as well as tools that display all the functions that a given library provides. The <tt>ldd</tt> command provides the list of all the shared libraries that a particular application is using. This can prove helpful if you are trying to track the number and location of the libraries that an application uses. Linux also provides the <tt>objdump</tt> <a name="iddle1936"></a><a name="iddle1937"></a><a name="iddle1938"></a><a name="iddle1939"></a>command, which enables you to search through a given library or application to display all the functions that it provides. By combining the <a name="iddle1940"></a><a name="iddle1941"></a><a name="iddle1942"></a><tt>ldd</tt> and <tt>objdump</tt> commands, you can take the output of <tt>ltrace</tt>, which only provides the names of the functions that an application calls, and determine which library a given function is part of.

<a name="ch08lev2sec4"></a>

#### 8.1.4\. Creating and Debugging Applications

Finally, Linux also <a name="iddle1943"></a><a name="iddle1944"></a><a name="iddle1945"></a><a name="iddle1946"></a><a name="iddle1947"></a>provides tools that enable you to create performance-tool-friendly applications, in addition to tools that enable you to interactively debug and investigate the attributes of running applications. The GNU compiler collection (<tt>gcc</tt>) can insert debugging information into applications that aid <tt>oprofile</tt> in finding the exact line and source file of a specific performance problem. In addition, the GNU debugger (gdb) <a name="iddle1948"></a><a name="iddle1949"></a><a name="iddle1950"></a><a name="iddle1951"></a><a name="iddle1952"></a>can also be used to find information about running applications not available by default to various performance tools.