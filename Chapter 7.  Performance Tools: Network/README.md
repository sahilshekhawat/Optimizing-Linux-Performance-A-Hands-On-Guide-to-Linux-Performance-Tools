## Chapter 7\. Performance Tools: Network

This chapter introduces some of the network performance tools available on Linux. We primarily focus on the tools that analyze the network traffic on a single box rather than network-wide management tools. Although network performance evaluation usually does not make sense in total isolation (that is, nodes do not normally talk to themselves), it is valuable to investigate the behavior of a single system on the network to identify local configuration and application problems. In addition, understanding the characteristics of network traffic on a single system can help to locate other problem systems, or local hardware and applications errors that slow down network performance.

After reading this chapter, you should be able to

*   Determine the speed and duplex settings of the Ethernet devices in the system (<tt>mii-tool</tt>, <tt>ethtool</tt>).

*   Determine the amount of network traffic flowing over each Ethernet interface (<tt>ifconfig</tt>, <tt>sar</tt>, <tt>gkrellm</tt>, <tt>iptraf</tt>, <tt>netstat</tt>, <tt>etherape</tt>).

*   Determine the types of IP traffic flowing in to and out of the system (<tt>gkrellm</tt>, <tt>iptraf</tt>, <tt>netstat</tt>, <tt>etherape</tt>).

*   Determine the amount of each type of IP traffic flowing in to and out of the system (<tt>gkrellm</tt>, <tt>iptraf</tt>, <tt>etherape</tt>).

*   Determine which applications are generating IP traffic (<tt>netstat</tt>).