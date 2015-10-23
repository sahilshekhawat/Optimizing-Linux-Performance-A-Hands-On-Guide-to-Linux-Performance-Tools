### 7.2\. Network Performance Tools

This section describes the Linux network performance tools available to diagnose performance problems. We start with the tools to determine the lowest level of network performance (physical statistics) and add tools that can investigate the layers above that.

<a name="ch07lev2sec3"></a>

#### 7.2.1\. mii-tool (Media-Independent Interface Tool)

<tt>mii-tool</tt> is an <a name="iddle1675"></a><a name="iddle1676"></a><a name="iddle1677"></a><a name="iddle1678"></a>Ethernet-specific hardware tool primarily used to configure an Ethernet device, but it can also provide information about the current configuration. This information, such as the link speed and duplex setting, can be useful when tracking down the cause of an under-performing network device.

<a name="ch07lev3sec1"></a>

##### 7.2.1.1 Network I/O Performance-Related Options

<tt>mii-tool</tt> requires root access to be used. It is invoked with the following <a name="iddle1679"></a><a name="iddle1680"></a><a name="iddle1681"></a><a name="iddle1682"></a>command line:

<pre>mii-tool [-v] [device]

</pre>

<tt>mii-tool</tt> prints the Ethernet settings for the given device. If no devices are specified, <tt>mii-tool</tt> displays information about all the available Ethernet devices. If the <tt>-v</tt> option is used, <tt>mii-tool</tt> displays verbose statistics about the offered and negotiated network capabilities.

<a name="ch07lev3sec2"></a>

##### 7.2.1.2 Example Usage

[Listing 7.1](ch07lev1sec2.html#ch07ex01) shows <a name="iddle1683"></a><a name="iddle1684"></a><a name="iddle1685"></a><a name="iddle1686"></a>the configuration of <tt>eth0</tt> on the system. The first line tells us that the Ethernet device is currently using a 100BASE-T full-duplex connection. The next few lines describe the capabilities of the network card in the machine and the capabilities that the card has detected of the network device on the other end of the wire.

<a name="ch07ex01"></a>

##### Listing 7.1\.

<pre>[root@nohs linux-2.6.8-1.521]# /sbin/mii-tool -v eth0

<span class="docEmphStrong">eth0: negotiated 100baseTx-FD, link ok</span>

  product info: vendor 00:00:00, model 0 rev 0

  basic mode:   autonegotiation enabled

  basic status: autonegotiation complete, link ok

  capabilities: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD

  advertising:  100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD flow-control

  link partner: 100baseTx-FD 100baseTx-HD 10baseT-FD 10baseT-HD

</pre>

<tt>mii-tool</tt> provides low-level information about how the physical level of the etheRnet device is <a name="iddle1687"></a><a name="iddle1688"></a><a name="iddle1689"></a><a name="iddle1690"></a>configured.

<a name="ch07lev2sec4"></a>

#### 7.2.2\. ethtool

<tt>ethtool</tt> provides <a name="iddle1691"></a><a name="iddle1692"></a><a name="iddle1693"></a><a name="iddle1694"></a>similar capabilities to <tt>mii-tool</tt> for configuration and display of statistics for Ethernet devices. However, <tt>ethtool</tt> is the more powerful tool and contains more configuration options and device statistics.

<a name="ch07lev3sec3"></a>

##### 7.2.2.1 Network I/O Performance-Related Options

<tt>ethtool</tt> requires root access to be used. It is invoked with the following command line:

<pre>ethtool [device]

</pre>

<tt>ethtool</tt> prints out configuration information about the given Ethernet device. If no devices are provided, <tt>ethtool</tt> prints statistics for all the Ethernet devices in the system. The options to change the current Ethernet settings are described in detail in the <tt>ethtool</tt> main <a name="iddle1695"></a><a name="iddle1696"></a><a name="iddle1697"></a><a name="iddle1698"></a>page.

<a name="ch07lev3sec4"></a>

##### 7.2.2.2 Example Usage

[Listing 7.2](ch07lev1sec2.html#ch07ex02) shows the <a name="iddle1699"></a><a name="iddle1700"></a><a name="iddle1701"></a><a name="iddle1702"></a>configuration of <tt>eth0</tt> on the system. Although the device supports many different speed and link settings, it is currently connected to a full-duplex 1,000Mbps link.

<a name="ch07ex02"></a>

##### Listing 7.2\.

<pre>[root@scrffy tmp]# /sbin/ethtool eth0

Settings for eth0:

        Supported ports: [ TP ]

        Supported link modes:   10baseT/Half 10baseT/Full

                                100baseT/Half 100baseT/Full

                                1000baseT/Half 1000baseT/Full

        Supports auto-negotiation: Yes

        Advertised link modes:  10baseT/Half 10baseT/Full

                                100baseT/Half 100baseT/Full

                                1000baseT/Half 1000baseT/Full

        Advertised auto-negotiation: Yes

        <span class="docEmphStrong">Speed: 1000Mb/s</span>

        Duplex: Full

        Port: Twisted Pair

        PHYAD: 0

        Transceiver: internal

        Auto-negotiation: on

        Supports Wake-on: g

        Wake-on: d

        Link detected: yes

</pre>

<tt>ethtool</tt> is simple to run, and it can quickly provide information about an improperly configured network <a name="iddle1703"></a><a name="iddle1704"></a><a name="iddle1705"></a><a name="iddle1706"></a>device.

<a name="ch07lev2sec5"></a>

#### 7.2.3\. ifconfig (Interface Configure)

The primary <a name="iddle1707"></a><a name="iddle1708"></a><a name="iddle1709"></a>job of <tt>ifconfig</tt> is to set up and configure the network interfaces in a Linux box. It also provides rudimentary performance statistics about all the network devices in the system. <tt>ifconfig</tt> is available on almost every Linux machine that uses networking.

<a name="ch07lev3sec5"></a>

##### 7.2.3.1 Network I/O Performance-Related Options

<tt>ifconfig</tt> is invoked with the following command line:

<pre>ifconfig [device]

</pre>

If no device is <a name="iddle1710"></a><a name="iddle1711"></a><a name="iddle1712"></a>specified, <tt>ifconfig</tt> shows statistics about all the active network devices. [Table 7-1](ch07lev1sec2.html#ch07table01) describes the performance statistics that <tt>ifconfig</tt> provides.

<a name="ch07table01"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-1\. Performance-Specific <span class="docEmphasis"><tt>ifconfig</tt></span> Statistics

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1713"></a><tt>RX packets</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The number of packets that this device has received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>TX packets</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1714"></a>The number of packets that this device has transmitted.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>errors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1715"></a>The number of errors when transmitting or receiving.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>dropped</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1716"></a>The number of dropped packets when transmitting or receiving.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>overruns</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1717"></a>The number of times the network device did not have enough buffer space to send or receive a packet.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>frame</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1718"></a>The number of low-level Ethernet frame errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>carrier</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1719"></a>The number of packets discarded because of link media failure (such as a faulty cable).

</td>

</tr>

</tbody>

</table>

Although primarily for network configuration, <tt>ifconfig</tt> provides a reasonable number of statistics that you can use to determine the health and performance of each of the network devices in the <a name="iddle1720"></a><a name="iddle1721"></a><a name="iddle1722"></a>system.

<a name="ch07lev3sec6"></a>

##### 7.2.3.2 Example Usage

[Listing 7.3](ch07lev1sec2.html#ch07ex03) shows the <a name="iddle1723"></a><a name="iddle1724"></a><a name="iddle1725"></a><a name="iddle1726"></a>network performance statistics from all the devices in the system. In this case, we have an Ethernet card (<tt>eth0</tt>) and the loopback (<tt>lo</tt>) device. In this example, the Ethernet card has received ~790Mb of data and has transmitted ~319Mb.

<a name="ch07ex03"></a>

##### Listing 7.3\.

<pre>[ezolt@wintermute tmp]$ /sbin/ifconfig

eth0      Link encap:Ethernet  HWaddr 00:02:E3:15:A5:03

          inet addr:192.168.0.4  Bcast:192.168.0.255  Mask:255.255.255.0

          UP BROADCAST NOTRAILERS RUNNING  MTU:1500  Metric:1

          RX packets:1047040 errors:0 dropped:0 overruns:0 frame:0

          TX packets:796733 errors:12 dropped:0 overruns:12 carrier:12

          collisions:0 txqueuelen:1000

          RX bytes:829403956 (790.9 Mb)  TX bytes:334962327 (319.4 Mb)

          Interrupt:19 Base address:0x3000

lo        Link encap:Local Loopback

          inet addr:127.0.0.1  Mask:255.0.0.0

          UP LOOPBACK RUNNING  MTU:16436 Metric:1

          RX packets:102 errors:0 dropped:0 overruns:0 frame:0

          TX packets:102 errors:0 dropped:0 overruns:0 carrier:0

          collisions:0 txqueuelen:0

          RX bytes:6492 (6.3 Kb)  TX bytes:6492 (6.3 Kb)

</pre>

The statistics provided by <tt>ifconfig</tt> represent the cumulative amount since system boot. If you bring down a network device and then bring it back up, the statistics do not reset. If you run <tt>ifconfig</tt> at regular intervals, you can eyeball the rate of change in the various statistics. You can automate this by using the watch command or a shell script, both of which are described in the next <a name="iddle1727"></a><a name="iddle1728"></a><a name="iddle1729"></a><a name="iddle1730"></a>chapter.

<a name="ch07lev2sec6"></a>

#### 7.2.4\. ip

Some of the network tools, such as <tt>ifconfig</tt>, are being phased out in favor of the new command: <tt>ip</tt>. <tt>ip</tt> <a name="iddle1731"></a><a name="iddle1732"></a><a name="iddle1733"></a><a name="iddle1734"></a>enables you to configure many different aspect of Linux networking, but it can also display performance statistics about each network device.

<a name="ch07lev3sec7"></a>

##### 7.2.4.1 Network I/O Performance-Related Options

When extracting performance statistics, you invoke <tt>ip</tt> with the following command line:

<pre>ip -s [-s] link

</pre>

If you call <tt>ip</tt> with these options, it prints statistics about all the network devices in the system, including the loopback (<tt>lo</tt>) and simple Internet transition (<tt>sit0</tt>) device. The <tt>sit0</tt> device allows IPv6 packets to be encapsulated in IPv4 packets and exists to ease the transition between IPv4 and IPv6\. If the extra <tt>-s</tt> is provided to <tt>ip</tt>, it provides a more detailed list of <a name="iddle1735"></a><a name="iddle1736"></a><a name="iddle1737"></a><a name="iddle1738"></a>low-level <a name="iddle1739"></a><a name="iddle1740"></a><a name="iddle1741"></a><a name="iddle1742"></a>Ethernet statistics. [Table 7-2](ch07lev1sec2.html#ch07table02) describes some of the performance statistics provided by <tt>ip</tt>.

<a name="ch07table02"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-2\. Network Performance <tt>ip</tt> Output Statistics

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Column

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>bytes</tt>

</td>

<td class="docTableCell" align="left" valign="top">

The total number of bytes sent or received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>packets</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1743"></a>The total number of packets sent or received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>errors</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1744"></a>The number of errors that occurred when transmitting or receiving.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>dropped</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1745"></a>The number of packets that were not sent or received as a result of a lack of resources on the network card.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>overruns</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1746"></a>The number of times the network did not have enough buffer space to send or receive more packets.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>mcast</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1747"></a>The number of multicast packets that have been received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>carrier</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1748"></a>The number of packets discarded because of link media failure (such as a faulty cable).

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>collsns</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1749"></a>This is the number of collisions that the device experienced when transmitting. These occur when two devices are trying to use the network at the exact same time.

</td>

</tr>

</tbody>

</table>

<tt>ip</tt> is a very versatile tool for Linux network configuration, and although its main function is the configuration of the <a name="iddle1750"></a><a name="iddle1751"></a><a name="iddle1752"></a><a name="iddle1753"></a>network, you can use it to extract low-level device statistics as well.

<a name="ch07lev3sec8"></a>

##### 7.2.4.2 Example Usage

[Listing 7.4](ch07lev1sec2.html#ch07ex04) shows <a name="iddle1754"></a><a name="iddle1755"></a><a name="iddle1756"></a><a name="iddle1757"></a>the network performance statistics from all the devices in the system. In this case, we have an Ethernet card, the loopback device, and the <tt>sit0</tt> tunnel device. In this example, the Ethernet card has received ~820Mb of data and has transmitted ~799Mb.

<a name="ch07ex04"></a>

##### Listing 7.4\.

<pre>[ezolt@nohs ezolt]$ /sbin/ip -s link

1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue

    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

    RX: bytes  packets  errors  dropped overrun mcast

    4460       67       0       0       0       0

    TX: bytes  packets  errors  dropped carrier collsns

    4460       67       0       0       0       0

2: eth0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast qlen 1000

    link/ether 00:10:b5:59:2c:82 brd ff:ff:ff:ff:ff:ff

    <span class="docEmphStrong">RX: bytes  packets  errors  dropped overrun mcast

    799273378  920999   0       0       0       0

    TX: bytes  packets  errors  dropped carrier collsns

    820603574  930929   0       0       0       0</span>

3: sit0: <NOARP> mtu 1480 qdisc noop

    link/sit 0.0.0.0 brd 0.0.0.0

    RX: bytes  packets  errors  dropped overrun mcast

    0          0        0       0       0       0

    TX: bytes  packets  errors  dropped carrier collsns

    0          0        0       0       0       0

</pre>

Much like <tt>ifconfig</tt>, <tt>ip</tt> provides system totals for statistics since the system has booted. If you use watch (described in the next chapter), you can <a name="iddle1758"></a><a name="iddle1759"></a><a name="iddle1760"></a><a name="iddle1761"></a>monitor how these values change over time.

<a name="ch07lev2sec7"></a>

#### 7.2.5\. sar

As discussed in <a name="iddle1762"></a><a name="iddle1763"></a><a name="iddle1764"></a>previous chapters, <tt>sar</tt> is one of the most versatile Linux performance tools. It can monitor many different things, archive statistics, and even display information in a format that is usable by other tools. <tt>sar</tt> does not always provide as much detail as the area-specific performance tools, but it provides a good overview.

Network performance statistics are no different. <tt>sar</tt> provides information about the link-level performance of the network, as do <tt>ip</tt> and <tt>ifconfig</tt>; however, it also provides some rudimentary statistics about the number of sockets opened by the transport layer.

<a name="ch07lev3sec9"></a>

##### 7.2.5.1 Network I/O Performance-Related Options

<tt>sar</tt> collects network statistics using the following <a name="iddle1765"></a><a name="iddle1766"></a><a name="iddle1767"></a>command:

<pre>sar [-n DEV | EDEV | SOCK | FULL ] [DEVICE] [interval] [count]

</pre>

<tt>sar</tt> collects many different types of performance statistics. [Table 7-3](ch07lev1sec2.html#ch07table03) describes the command-line options used by <tt>sar</tt> to display network performance statistics.

<a name="ch07table03"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-3\. <span class="docEmphasis"><tt>sar</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n DEV</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1768"></a>Shows statistics about the number of packets and bytes sent and received by each device.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n EDEV</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1769"></a>Shows information about the transmit and receive errors for each device.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n SOCK</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1770"></a>Shows information about the total number of sockets (TCP, UDP, and RAW) in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n FULL</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1771"></a>Shows all the network statistics.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>interval</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1772"></a>The length of time between samples.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>count</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1773"></a>The total number of samples to take.

</td>

</tr>

</tbody>

</table>

The network performance options that <tt>sar</tt> provides are <a name="iddle1774"></a><a name="iddle1775"></a><a name="iddle1776"></a>described in [Table 7-4](ch07lev1sec2.html#ch07table04).

<a name="ch07table04"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-4\. <span class="docEmphasis"><tt>sar</tt></span> Network Performance Statistics

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1777"></a><a name="iddle1778"></a><a name="iddle1779"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxpck/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1780"></a>The rate of packets received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txpck/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1781"></a>The rate of packets sent.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxbyt/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1782"></a>The rate of bytes received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txbyt/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1783"></a>The rate of bytes sent.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxcmp/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1784"></a>The rate of compressed packets received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txcmp/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1785"></a>The rate of compressed packets sent.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxmcst/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1786"></a>The rate of multicast packets received.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxerr/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1787"></a>The rate of receive errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txerr/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1788"></a>The rate of transmit errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>coll/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1789"></a>The rate of Ethernet collisions when transmitting.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxdrop/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1790"></a>The rate of received frames dropped due to Linux kernel buffer shortages.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txdrop/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1791"></a>The rate of transmitted frames dropped due to Linux kernel buffer shortages.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txcarr/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1792"></a>The rate of transmitted frames dropped due to carrier errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxfram/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1793"></a>The rate of received frames dropped due to frame-alignment errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rxfifo/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1794"></a>The rate of received frames dropped due to FIFO errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>txfifo/s</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1795"></a>The rate of transmitted frames dropped due to FIFO errors.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>totsck</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1796"></a>The total number of sockets in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>tcpsck</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1797"></a>The total number of TCP sockets in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>udpsck</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1798"></a>The total number of UDP sockets in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>rawsck</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1799"></a>The total number of RAW sockets in use.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>ip-frag</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1800"></a>The total number of IP fragments.

</td>

</tr>

</tbody>

</table>

Considering all the statistics that <tt>sar</tt> can gather, it really does provide the most system-level performance statistics in a single <a name="iddle1801"></a><a name="iddle1802"></a><a name="iddle1803"></a>location.

<a name="ch07lev3sec10"></a>

##### 7.2.5.2 Example Usage

In [Listing 7.5](ch07lev1sec2.html#ch07ex05), we examine <a name="iddle1804"></a><a name="iddle1805"></a><a name="iddle1806"></a><a name="iddle1807"></a>the transmit and receive statistics of all the network devices in the system. As you can see, the <tt>eth0</tt> device is the most active. In the first sample, <tt>eth0</tt> is receiving ~63,000 bytes per second (<tt>rxbyt/s</tt>) and transmitting ~45,000 bytes per second (<tt>txbyt/s</tt>). No compressed packets are sent (<tt>txcmp</tt>) or received (<tt>rxcmp</tt>). (Compressed packets are usually present during SLIP or PPP connections.)

<a name="ch07ex05"></a>

##### Listing 7.5\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -n DEV 1 2

Linux 2.4.22-1.2174.nptlsmp (wintermute.phil.org)      06/07/04

21:22:29  IFACE   rxpck/s   txpck/s   rxbyt/s   txbyt/s  rxcmp/s  txcmp/s rxmcst/s

21:22:30     lo      0.00      0.00      0.00      0.00     0.00     0.00     0.00

21:22:30   eth0     68.00     65.00  63144.00  45731.00     0.00     0.00     0.00

21:22:30  IFACE   rxpck/s   txpck/s   rxbyt/s   txbyt/s  rxcmp/s  txcmp/s  rxmcst/s

21:22:31     lo      0.00      0.00      0.00      0.00     0.00     0.00      0.00

21:22:31   eth0     80.39     47.06  45430.39  30546.08     0.00     0.00      0.00

Average:  IFACE   rxpck/s   txpck/s   rxbyt/s   txbyt/s  rxcmp/s  txcmp/s  rxmcst/s

Average:     lo      0.00      0.00      0.00      0.00     0.00     0.00      0.00

Average:   eth0     74.26     55.94  54199.50  38063.37     0.00     0.00      0.00

</pre>

In [Listing 7.6](ch07lev1sec2.html#ch07ex06), we examine the number of open sockets in the system. We can see the total number of open sockets and the TCP, RAW, and UDP sockets. <tt>sar</tt> also displays the number of fragmented IP <a name="iddle1808"></a><a name="iddle1809"></a><a name="iddle1810"></a><a name="iddle1811"></a>packets.

<a name="ch07ex06"></a>

##### Listing 7.6\.

<pre>[ezolt@wintermute sysstat-5.0.2]$ sar -n SOCK 1 2

Linux 2.4.22-1.2174.nptlsmp (wintermute.phil.org)    06/07/04

21:32:26    totsck   tcpsck   udpsck   rawsck   ip-frag

21:32:27       373      118        8        0         0

21:32:28       373      118        8        0         0

Average:       373      118        8        0         0

</pre>

<tt>sar</tt> provides a good overview of the system's performance. However, when we are investigating a performance problem, we really want to understand what processes or services are consuming a particular resource. <tt>sar</tt> does not provide this level of detail, but it does enable us to observe the overall system <a name="iddle1812"></a><a name="iddle1813"></a><a name="iddle1814"></a><a name="iddle1815"></a>network I/O statistics.

<a name="ch07lev2sec8"></a>

#### 7.2.6\. gkrellm

<tt>gkrellm</tt> is a <a name="iddle1816"></a><a name="iddle1817"></a><a name="iddle1818"></a>graphical monitor that enables you to keep an eye on many different system performance statistics. It draws charts of different performance statistics, including CPU usage, disk I/O, and network usage. It can be "themed" to change its appearance, and even accepts plug-ins to monitor events not included in the default release.

<tt>gkrellm</tt> provides similar information to <tt>sar</tt>, <tt>ip</tt>, and <tt>ipconfig</tt>, but unlike the other tools, it provides a graphical view of the data. In addition, it can provide information about the traffic flowing through particular UDP and TCP ports. This is the first tool that we have seen that can show which services are consuming different amounts of network bandwidth.

<a name="ch07lev3sec11"></a>

##### 7.2.6.1 Network I/O Performance-Related Options

<tt>gkrellm</tt> is invoked using the following command line:

<pre>gkrellm

</pre>

None of <tt>gkrellm's</tt> command-line options configure the statistics that it monitors. You do all configurations graphically after <tt>gkrellm</tt> is started. To bring up the configuration screen, you can either right-click the <tt>gkrellm's</tt> title bar and select Configuration, or just press F1 when your cursor is in any area of the window. This brings up a configuration window (see <a name="iddle1819"></a><a name="iddle1820"></a><a name="iddle1821"></a>[Figure 7-1](ch07lev1sec2.html#ch07fig01)).

<a name="ch07fig01"></a>

<center>

##### Figure 7-1\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig01_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig01_alt.jpg)

[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig01_alt.jpg)[Figure 7-2](ch07lev1sec2.html#ch07fig02) shows the network configuration window. It is used to configure which statistics <a name="iddle1822"></a><a name="iddle1823"></a><a name="iddle1824"></a>and which devices are shown in the final <tt>gkrellm</tt> output window.

<a name="ch07fig02"></a>

<center>

##### Figure 7-2\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig02_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig02_alt.jpg)

[You can configure <tt>gkrellm</tt> to monitor the activity on a particular range of TCP ports. Doing so enables you to monitor the exact ports used by services such as HTTP or FTP and to measure the amount of bandwidth that they are using. In](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig02_alt.jpg) [Figure 7-2](ch07lev1sec2.html#ch07fig02), we have configured <tt>gkrellm</tt> to monitor the ports used by the bittorrent (BT) P2P application and the Web server (HTTP).

<tt>gkrellm</tt> is a flexible and powerful graphical performance-monitoring tool. It enables you to see how the system is currently performing and how its performance changes over time. The most difficult aspect of using <tt>gkrellm</tt> is reading the small default text. However, the appearance of <tt>gkrellm</tt> can be easily themed, so presumably, this could be easily <a name="iddle1825"></a><a name="iddle1826"></a><a name="iddle1827"></a>fixed.

<a name="ch07lev3sec12"></a>

##### 7.2.6.2 Example Usage

As stated <a name="iddle1828"></a><a name="iddle1829"></a><a name="iddle1830"></a>previously, <tt>gkrellm</tt> can monitor many different types of events. In [Figure 7-3](ch07lev1sec2.html#ch07fig03), we pruned the output so that only statistics relevant to network traffic and use is displayed.

<a name="ch07fig03"></a>

<center>

##### Figure 7-3\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig03.jpg)

</center>

As you can see in [Figure 7-3](ch07lev1sec2.html#ch07fig03), the top two graphs are the bandwidth used for the ports (BT and HTTP) that we set up in the configuration section, and the bottom two graphics are the statistics for each of the network devices (<tt>eth0</tt> and <tt>lo</tt>). There is a small amount of bittorrent (BT) traffic, but no Web server traffic (HTTP). The Ethernet device <tt>eth0</tt> had some large activity in the past, but is settling down now. The lighter shade in the <tt>eth0</tt> indicates the number of bytes received, and the darker shade indicates the number of bytes transmitted.

<tt>gkrellm</tt> is a powerful graphical tool that makes it easy to diagnose the status of the system at a <a name="iddle1831"></a><a name="iddle1832"></a><a name="iddle1833"></a>glance.

<a name="ch07lev2sec9"></a>

#### 7.2.7\. iptraf

<tt>iptraf</tt> is a real-time <a name="iddle1834"></a><a name="iddle1835"></a><a name="iddle1836"></a>network monitoring tool. It provides a large number of modes to monitor network interfaces and traffic. <tt>iptraf</tt> is a console application, but its user interface is a cursor-based series of menus and windows.

Like the other tools mentioned previously in this chapter, it can provide information about the rate at which each network device is sending frames. However, it can also display information about the type and size of the TCP/IP packet and about which ports are being used for network traffic.

<a name="ch07lev3sec13"></a>

##### 7.2.7.1 Network I/O Performance-Related Options

<tt>iptraf</tt> is invoked with the following command line:

<pre>iptraf [-d interface] [-s interface] [-t <minutes>]

</pre>

If <tt>iptraf</tt> is called with no parameters, it brings up a menu that enables you to select the interface to monitor and type of information that you want to monitor. [Table 7-5](ch07lev1sec2.html#ch07table05) describes the command-line parameters that enable you to see the amount of network traffic on a particular interface or network service.

<a name="ch07table05"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-5\. <span class="docEmphasis"><tt>iptraf</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1837"></a><a name="iddle1838"></a><a name="iddle1839"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-d interface</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1840"></a>Detailed statistics for an interface including receive, transmit, and error rates

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-s interface</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1841"></a>Statistics about which IP ports are being used on an interface and how many bytes are flowing through them

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-t <minutes></tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1842"></a>Number of minutes that <tt>iptraf</tt> runs before exiting

</td>

</tr>

</tbody>

</table>

<tt>iptraf</tt> has many more modes and configuration <a name="iddle1843"></a><a name="iddle1844"></a><a name="iddle1845"></a>options. Read its included documentation for more information.

<a name="ch07lev3sec14"></a>

##### 7.2.7.2 Example Usage

<tt>iptraf</tt> creates <a name="iddle1846"></a><a name="iddle1847"></a><a name="iddle1848"></a>a display similar to [Figure 7-4](ch07lev1sec2.html#ch07fig04) when it is invoked with the following command:

<pre>[root@wintermute tmp]# iptraf -d eth0 -t 1

</pre>

<a name="ch07fig04"></a>

<center>

##### Figure 7-4\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig04.jpg)

</center>

This command specifies that <tt>iptraf</tt> should display detailed statistics about Ethernet device <tt>eth0</tt> and exit after it has run for 1 minute. In this case, we can see that 186.8kbps are received and 175.5kbps are transmitted by the <tt>eth0</tt> network device.

The next <a name="iddle1849"></a><a name="iddle1850"></a><a name="iddle1851"></a>command, whose results are shown in [Figure 7-5](ch07lev1sec2.html#ch07fig05), asks <tt>iptraf</tt> to show information about the amount of network traffic from each UDP or TCP port. <tt>iptraf</tt> was invoked with the following command:

<a name="ch07fig05"></a>

<center>

##### Figure 7-5\.

![](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig05.jpg)

</center>

<pre>[root@wintermute etherape-0.9.0]# iptraf -s eth0 -t 10

</pre>

Because the TCP or UDP ports of well-known services are fixed, you can use this to determine how much traffic each service is handling. [Figure 7-5](ch07lev1sec2.html#ch07fig05) shows that 29kb of HTTP data has been sent from <tt>eth0</tt> and 25kb has been received.

Because <a name="iddle1852"></a><a name="iddle1853"></a><a name="iddle1854"></a><tt>iptraf</tt> is a console-based application, it doesn't require an X server or X server libraries. Even though <tt>iptraf</tt> cannot be controlled with a mouse, it is easy to use and configurable.

<a name="ch07lev2sec10"></a>

#### 7.2.8\. netstat

<tt>netstat</tt> is a basic network-performance tool that is present on nearly every Linux machine with <a name="iddle1855"></a><a name="iddle1856"></a><a name="iddle1857"></a>networking. You can use it to extract information about the number and types of network sockets currently being used and interface-specific statistics regarding the number of UDP or TCP packets flowing to and from the current system. It also enables you to trace the owner of a socket back to a particular process or PID, which can prove useful when trying to determine the application responsible for network traffic.

<a name="ch07lev3sec15"></a>

##### 7.2.8.1 Network I/O Performance-Related Options

<tt>netstat</tt> is invoked with the following command line:

<pre>netstat [-p] [-c] [–interfaces=<name>] [-s] [-t] [-u] [-w]

</pre>

If <tt>netstat</tt> is <a name="iddle1858"></a><a name="iddle1859"></a><a name="iddle1860"></a>called without any parameters, it shows information about system-wide socket usage and displays information about both Internet and UNIX domain sockets. (UNIX domain sockets are used for interprocess communication on the local machine, but do not indicate network traffic.) To retrieve all the statistics that <tt>netstat</tt> is capable of displaying, you must run it as root. [Table 7-6](ch07lev1sec2.html#ch07table06) describes the command-line options of <tt>netstat</tt> that modify the types of network statistics that <tt>netstat</tt> displays.

<a name="ch07table06"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-6\. <span class="docEmphasis"><tt>netstat</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

<a name="iddle1861"></a><a name="iddle1862"></a><a name="iddle1863"></a>Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-p</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1864"></a>Displays the PID/program name responsible for opening each of the displayed sockets

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-c</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1865"></a>Continually updates the display of information every second

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--interfaces=<name></tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1866"></a>Displays network statistics for the given interface

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--statistics|</tt>-s

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1867"></a>IP/UDP/ICMP/TCP statistics

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--tcp|</tt>-t

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1868"></a>Shows only information about TCP sockets

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--udp|</tt>-u

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1869"></a>Shows only information about UDP sockets.

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>--raw|</tt>-w

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1870"></a>Shows only information about RAW sockets (IP and ICMP)

</td>

</tr>

</tbody>

</table>

<tt>netstanetstat</tt> also accepts some command-line options not described here. See the <tt>netstat</tt> man page for more <a name="iddle1871"></a><a name="iddle1872"></a><a name="iddle1873"></a>details.

<a name="ch07lev3sec16"></a>

##### 7.2.8.2 Example Usage

[Listing 7.7](ch07lev1sec2.html#ch07ex07) asks <tt>netstat</tt> to show the active TCP connections and to continually update this information. Every second, <tt>netstat</tt> displays new TCP network statistics. <tt>netstat</tt> does not enable you to set the length of time that it will monitor, so it will only stop if it is killed or interrupted (Ctrl-C).

<a name="ch07ex07"></a>

##### Listing 7.7\.

<pre>[root@wintermute ezolt]# netstat -t -c

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address          Foreign Address         State

tcp        0      0 192.168.0.4:1023       fas.harvard.edu:ssh     ESTABLISHED

tcp        0      0 192.168.0.4:32844      216.239.39.147:http     TIME_WAIT

tcp        0      0 192.168.0.4:32843      216.239.39.147:http     TIME_WAIT

tcp        0      0 192.168.0.4:32853      skaiste.elekta.lt:http  ESTABLISHED

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address          Foreign Address         State

tcp        0      0 192.168.0.4:1023       fas.harvard.edu:ssh     ESTABLISHED

tcp        0      0 192.168.0.4:32844      216.239.39.147:http     TIME_WAIT

tcp        0      0 192.168.0.4:32843      216.239.39.147:http     TIME_WAIT

tcp        0      0 192.168.0.4:32853      skaiste.elekta.lt:http  ESTABLISHED

</pre>

[Listing 7.8](ch07lev1sec2.html#ch07ex08) asks <a name="iddle1878"></a><a name="iddle1879"></a><a name="iddle1880"></a><a name="iddle1881"></a><tt>netstat</tt> to once again print the TCP socket information, but this time, we also ask it to display the program that is responsible for this socket. In this case, we can see that SSH and <tt>mozilla-bin</tt> are the applications that are initiating the TCP connections.

<a name="ch07ex08"></a>

##### Listing 7.8\.

<pre>[root@wintermute ezolt]# netstat -t -p

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address       Foreign Address        State       PID/Program name

tcp        0      0 192.168.0.4:1023    fas.harvard.edu:ssh    ESTABLISHED 1463/ssh

tcp        0      0 192.168.0.4:32844   216.239.39.147:http    TIME_WAIT -

tcp        0      0 192.168.0.4:32843   216.239.39.147:http    TIME_WAIT -

tcp        0      0 192.168.0.4:32853   skaiste.elekta.lt:http ESTABLISHED 1291/mozilla-bin

</pre>

[Listing 7.9](ch07lev1sec2.html#ch07ex09) asks <tt>netstat</tt> to provide statistics about the UDP traffic that the system has received since <a name="iddle1882"></a><a name="iddle1883"></a><a name="iddle1884"></a><a name="iddle1885"></a>boot.

<a name="ch07ex09"></a>

##### Listing 7.9\.

<pre>[root@wintermute ezolt]# netstat -s -u

Udp:

    125 packets received

    0 packets to unknown port received.

    0 packet receive errors

    152 packets sent

</pre>

[Listing 7.10](ch07lev1sec2.html#ch07ex10) asks <tt>netstat</tt> to provide information about the amount of network traffic flowing through the <tt>eth0</tt> <a name="iddle1886"></a><a name="iddle1887"></a><a name="iddle1888"></a><a name="iddle1889"></a>interface.

<a name="ch07ex10"></a>

##### Listing 7.10\.

<pre>[root@wintermute ezolt]# netstat –interfaces=eth0

Kernel Interface table

Iface       MTU Met    RX-OK RX-ERR RX-DRP RX-OVR   TX-OK TX-ERR TX-DRP TX-OVR Flg

eth0       1500   0    52713      0      0      0   13711      1      0      1 BNRU

</pre>

<tt>netstat</tt> provides a great number of network performance statistics about sockets and interfaces in a running Linux system. It is the only network-performance tool that maps the sockets used back to the PID of the process that is using it, and is therefore very <a name="iddle1890"></a><a name="iddle1891"></a><a name="iddle1892"></a><a name="iddle1893"></a>useful.

<a name="ch07lev2sec11"></a>

#### 7.2.9\. etherape

<tt>etherape</tt> (a pun <a name="iddle1894"></a><a name="iddle1895"></a><a name="iddle1896"></a>on the Windows-based network tool <tt>etherman</tt>) provides a visualization of the current network traffic. By default, it observes <span class="docEmphasis">all</span> the network traffic flowing on the network, not just those packets that the current machine is sending or receiving. However, it can be configured to only display network information for the current machine.

<tt>etherape</tt> is a little rough around the edges (in interface and documentation), but it provides a unique visual insight into how the network is connected, what types of services are being requested, and which nodes are requesting them. It creates a graph whose nodes represent the systems on the network. The nodes that are communicating have lines connecting them that increase in size as more network traffic flows between them. As a particular system's network usage increases, the size of the circle representing that system also increases. The lines connecting the different systems are colored differently depending on the protocols they are using to communicate with each <a name="iddle1897"></a><a name="iddle1898"></a><a name="iddle1899"></a>other.

<a name="ch07lev3sec17"></a>

##### 7.2.9.1 Network I/O Performance-Related Options

<tt>etherape</tt> uses the <tt>libpcap</tt> library to capture the network packets and, as a result, it must be run as root. <tt>etherape</tt> is invoked using the following command line:

<pre>etherape [-n] [-i <interface name>]

</pre>

[Table 7-7](ch07lev1sec2.html#ch07table07) describes some of the command-line options that change the interface that <tt>etherape</tt> monitors and whether resolved host names are printed on each node.

<a name="ch07table07"></a>

<table cellspacing="0" frame="hsides" rules="none" cellpadding="5"><caption>

##### Table 7-7\. <span class="docEmphasis"><tt>etherape</tt></span> Command-Line Options

</caption><colgroup><col width="150"><col width="350"></colgroup>

<thead>

<tr>

<th class="thead" scope="col" align="left" valign="top">

Option

</th>

<th class="thead" scope="col" align="left" valign="top">

Explanation

</th>

</tr>

</thead>

<tbody>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-n, --numeric</tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1900"></a>Shows only the IP number of the hosts rather than the resolved names

</td>

</tr>

<tr>

<td class="docTableCell" align="left" valign="top">

<tt>-i, --interface=<interface name></tt>

</td>

<td class="docTableCell" align="left" valign="top">

<a name="iddle1901"></a>Specifies the interface that will be monitored

</td>

</tr>

</tbody>

</table>

All in all, <tt>etherape</tt>'s documentation is rather sparse. The <tt>etherape</tt> man page describes a few more command lines that change its appearance and behavior, but the best way to learn it is to try it. In general, <tt>etherape</tt> is a great way to visualize <a name="iddle1902"></a><a name="iddle1903"></a><a name="iddle1904"></a>the network.

<a name="ch07lev3sec18"></a>

##### 7.2.9.2 Example Usage

[Figure 7-6](ch07lev1sec2.html#ch07fig06) shows <tt>etherape</tt> monitoring a relatively simple network. If we match up the color of the protocol to the color of the biggest circle, we see that this node is generating a high amount of SSH traffic. From the figure, it can be difficult to determine which node is causing this SSH traffic. Although not pictured, if we double-click the big circle, <tt>etherape</tt> creates a window with statistics pertaining to the node responsible for the traffic. We can use this to investigate each of the generators of network traffic and investigate their node names.

<a name="ch07fig06"></a>

<center>

##### Figure 7-6\.

<div class="v1">[](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig06_alt.jpg)</div>

</center>

[  
](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig06_alt.jpg)

[<tt>etherape</tt>'s output](http://85.147.245.113/mirrorbooks/linuxperformanceguide/0131486829/0131486829/images/0131486829/graphics/07fig06_alt.jpg) <a name="iddle1908"></a><a name="iddle1909"></a><a name="iddle1910"></a>is periodically updated. As network traffic changes, its graph is updated. It can be fascinating just to watch the network traffic flow and see how it is used and changes over time.