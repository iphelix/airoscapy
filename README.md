Airoscapy is a passive wireless access point scanner similar to Kismet and Aircrack. The tool was built to demonstrate the power of [Scapy](/research/scapy) as a generic and powerful network monitoring library.

Scapy
====

The tool requires installation of [Scapy](/research/scapy). You can obtain [Scapy](/research/scapy) either directly from the developer <http://www.secdev.org/projects/scapy/> or use your operating system's packaging system to download and install it. For example, here is how you would set it up on an Ubuntu system:

    sudo apt-get install python-scapy

Setting up a monitor interface
==================

In order to detect Access Points without sending Probe requests, you must enable monitor mode on your card. On a modern linux system you can use **iw** wireless configuration utility to set up a monitor interface. Assuming you existing wireless card is identified as **wlan0** follow these commands to create a **mon0** monitoring interface:

    # iw dev wlan0 interface add mon0 type monitor
    # ifconfig mon0 up

Test whether you can capture packets by using **tcpdump**:

    # tcpdump -i mon0

You should see a stream of packets looking something like this:


    18:42:49.448730 1.0 Mb/s 2462 MHz 11b -82dB signal antenna 1 [bit 14] Beacon (linksys) [1.0* 2.0* 5.5* 11.0* 18.0 24.0 36.0 54.0 Mbit] ESS CH: 11, PRIVACY[|802.11]
    18:42:49.452508 2.0 Mb/s 2462 MHz 11b -76dB signal antenna 1 [bit 14] Beacon (cisco) [1.0* 2.0* 5.5 11.0 Mbit] ESS CH: 11, PRIVACY
    18:42:49.465215 1.0 Mb/s 2462 MHz 11b -78dB signal antenna 1 [bit 14] Beacon (buffalo) [1.0* 2.0* 5.5* 11.0* 6.0 9.0 12.0 18.0 Mbit] ESS CH: 11, PRIVACY[|802.11]
    ...

Running Airoscapy
============

Using Airoscapy is very straightforward. Simply specify a monitor interface as the first command line parameter and execute the tool with root privileges. Press CTRL-C to stop scanning.

    # python airoscapy.py mon0
    -=-=-=-=-=-= AIROSCAPY =-=-=-=-=-=-
    CH ENC BSSID             SSID
    11  Y  c0:c1:c0:12:34:56 caesars
    11  Y  00:24:01:12:34:56 cosmopolitan
    11  Y  c0:c1:c0:12:34:56 encore
    09  N  c0:c1:c0:12:34:56 excalibur
    09  Y  00:16:b6:12:34:56 flamingo
    05  N  00:16:b6:12:34:56 golden nugget
    01  Y  e0:91:f5:12:34:56 hard rock
    01  Y  00:22:3f:12:34:56 harrahs
    07  Y  00:1e:52:12:34:56 luxor
    07  Y  c0:3f:0e:12:34:56 mgm
    07  Y  00:30:bd:12:34:56 mirage
    10  Y  00:25:9c:12:34:56 nyny
    11  N  c0:c1:c0:12:34:56 palms
    11  Y  00:14:6c:12:34:56 rio
    ^C
    -=-=-=-=-=  STATISTICS =-=-=-=-=-=-
    Total APs found: 14
    Encrypted APs  : 11
    Unencrypted APs: 3



