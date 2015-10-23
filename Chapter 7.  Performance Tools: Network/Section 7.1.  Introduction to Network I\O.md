### 7.1\. Introduction to Network I/O

Network traffic <a name="iddle1623"></a><a name="iddle1624"></a><a name="iddle1625"></a>in Linux and every other major operating system is abstracted as a series of hardware and software layers. The link, or lowest, layer contains network hardware such as Ethernet <a name="iddle1626"></a>devices. When moving network traffic, this layer does not distinguish types of traffic but just transmits and receives data (or frames) as fast as possible.

Stacked above the <a name="iddle1627"></a>link layer is a network layer. This layer uses the Internet Protocol <a name="iddle1628"></a><a name="iddle1629"></a>(IP) and Internet Control Message Protocol <a name="iddle1630"></a><a name="iddle1631"></a>(ICMP) to address and route packets of data from machine to machine. IP/ICMP make their best-effort attempt to pass the packets between machines, but they make no guarantees about whether a packet actually arrives at its destination.

Stacked above the network layer is the transport layer, <a name="iddle1632"></a>which defines the Transport Control Protocol (TCP) <a name="iddle1633"></a><a name="iddle1634"></a>and User Datagram Protocol (UDP). TCP is a reliable protocol that guarantees that a message is either delivered over the network or generates an error if the message is not delivered. TCP's sibling protocol, UDP, is an unreliable protocol that deliberately (to achieve the highest data rates) does not guarantee message delivery. UDP and TCP add the concept of a "service" to IP. UDP and TCP receive messages on numbered "ports." By convention, each type of network service is assigned a different number. For example, Hypertext Transfer Protocol (HTTP) <a name="iddle1635"></a><a name="iddle1636"></a>is typically port 80, Secure Shell (SSH) <a name="iddle1637"></a><a name="iddle1638"></a>is typically port 22, and File Transport Protocol (FTP) <a name="iddle1639"></a><a name="iddle1640"></a>is typically port 23\. In a Linux system, the file <tt>/etc/services</tt> defines all the ports and the types of service they provide.

The final layer is the application layer. It includes all the different applications that use the layers below to transmit packets over the network. These include applications such Web servers, SSH clients, or even peer-to-peer (P2P) file-sharing clients such as bittorrent.

The lowest three layers (link, network, and transport) are implemented or controlled within the Linux kernel. The kernel provides statistics about how each layer is performing, including information about the bandwidth usage and error count as data flows through each of the layers. The tools covered in this chapter enable <a name="iddle1641"></a><a name="iddle1642"></a>you to extract and view those statistics.

<a name="ch07lev2sec1"></a>

#### 7.1.1\. Network Traffic in the Link Layer

At the <a name="iddle1643"></a><a name="iddle1644"></a><a name="iddle1645"></a><a name="iddle1646"></a>lowest levels of the network stack, Linux can detect the rate at which data traffic is flowing through the link layer. The link layer, which is typically Ethernet, sends information into the network as a series of frames. Even though the layers above may have pieces of information much larger than the frame size, the link layer breaks everything up into frames to send them over the network. This maximum size of data in a frame is known as the maximum transfer <a name="iddle1647"></a><a name="iddle1648"></a><a name="iddle1649"></a>unit (MTU). You can use network configuration tools such as <tt>ip</tt> or <tt>ifconfig</tt> to set the MTU. For Ethernet, the maximum size is commonly 1,500 bytes, although some hardware supports jumbo frames up to 9,000 bytes. The size of the MTU has a direct impact on the efficiency of the network. Each frame in the link layer has a small header, so using a large MTU increases the ratio of user data to overhead (header). When using a large MTU, however, each frame of data has a higher chance of being corrupted or dropped. For clean physical links, a high MTU usually leads to better performance because it requires less overhead; for noisy links, however, a smaller MTU may actually enhance performance because less data has to be re-sent when a single frame is <a name="iddle1650"></a><a name="iddle1651"></a><a name="iddle1652"></a><a name="iddle1653"></a>corrupted.

At the physical layer, frames flow <a name="iddle1654"></a><a name="iddle1655"></a><a name="iddle1656"></a><a name="iddle1657"></a><a name="iddle1658"></a>over the physical network; the Linux kernel collects a number of different statistics about the number and types of frames:

*   <span class="docEmphasis">Transmitted/received</span>— If the frame successfully flowed in to or out of the machine, it is counted as a transmitted or received frame.

*   <span class="docEmphasis">Errors</span>— Frames with errors (possibly because of a bad network cable or duplex mismatch).

*   <span class="docEmphasis">Dropped</span>— Frames that were discarded (most likely because of low amounts of memory or buffers).

*   <span class="docEmphasis">Overruns</span>— Frames that may have been discarded by the network card because the kernel or network card was overwhelmed with frames. This should not normally happen.

*   <span class="docEmphasis">Frame</span>— These frames were dropped as a result of problems on the physical level. This could be the result of cyclic redundancy check (CRC) errors <a name="iddle1659"></a><a name="iddle1660"></a>or other low-level problems.

*   <span class="docEmphasis">Multicast</span>— These frames are not directly addressed to the current system, but rather have been broadcast to a series of nodes simultaneously.

*   <span class="docEmphasis">Compressed</span>— Some lower-level interfaces, such as Point-to-Point Protocol (PPP) <a name="iddle1661"></a><a name="iddle1662"></a>or Serial Line Internet Protocol (SLIP) <a name="iddle1663"></a><a name="iddle1664"></a>devices compress frames before they are sent over the network. This value indicates the number of these compressed frames.

Several of the Linux network performance tools can display the number of frames of each type that have passed through each network device. These tools often require a device name, so it is important to understand how Linux names network devices to understand which name represents which device. Ethernet devices are named ethN, where eth0 is the first device, eth1 is the second device, and so on. PPP devices are named pppN in the same manner as Ethernet devices. The loopback device, which is used to network with the local machine, is named <tt>lo</tt>.

When investigating a performance problem, it is crucial to know the maximum speed that the underlying physical layer can support. For example, Ethernet devices commonly support multiple speeds, such 10Mbps, 100Mbps, or even 1,000Mbps. The underlying Ethernet cards and infrastructure (switches) must be capable of handling the required speed. Although most cards can autodetect the highest support speed and set themselves up appropriately, if a card or switch is misconfigured, performance will suffer. If the higher speed cannot be used, the Ethernet devices often negotiate down to a slower speed, but they continue to function. If network performance is much slower than expected, it is best to verify with tools such as <tt>ethtool</tt> and <tt>mii-tool</tt> that the Ethernet speeds are set to what you <a name="iddle1665"></a><a name="iddle1666"></a><a name="iddle1667"></a><a name="iddle1668"></a><a name="iddle1669"></a>expect.

<a name="ch07lev2sec2"></a>

#### 7.1.2\. Protocol-Level Network Traffic

For TCP or UDP traffic, Linux <a name="iddle1670"></a><a name="iddle1671"></a><a name="iddle1672"></a><a name="iddle1673"></a><a name="iddle1674"></a>uses the socket/port abstraction to connect two machines. When connecting to a remote machine, the local application uses a network socket to open a port on a remote machine. As mentioned previously, most common network services have an agreed-upon port number, so a given application will be able to connect to the correct port on the remote machine. For example, port 80 is commonly used for HTTP. When loading a Web page, browsers connect to port 80 on remote machines. The Web server of the remote machine listens for connections on port 80, and when a connection occurs, the Web server sets up the connection for transfer of the Web page.

The Linux network performance tools can track the amount of data that flows over a particular network port. Because port numbers are unique for each service, it is possible to determine the amount of network traffic flowing to a particular service.