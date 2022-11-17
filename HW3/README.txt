Task 1
Ans 1:
Output of Nodes:
mininet> nodes
available nodes are: 
h1 h2 h3 h4 h5 h6 h7 h8 s1 s2 s3 s4 s5 s6 s7

Output of net:
mininet> net
h1 h1-eth0:s3-eth2
h2 h2-eth0:s3-eth3
h3 h3-eth0:s4-eth2
h4 h4-eth0:s3-eth4
h5 h5-eth0:s6-eth2
h6 h6-eth0:s6-eth3
h7 h7-eth0:s7-eth2
h8 h8-eth0:s7-eth3
s1 lo:  s1-eth1:s2-eth1 s1-eth2:s5-eth1
s2 lo:  s2-eth1:s1-eth1 s2-eth2:s3-eth1 s2-eth3:s4-eth1
s3 lo:  s3-eth1:s2-eth2 s3-eth2:h1-eth0 s3-eth3:h2-eth0 s3-eth4:h4-eth0
s4 lo:  s4-eth1:s2-eth3 s4-eth2:h3-eth0
s5 lo:  s5-eth1:s1-eth2 s5-eth2:s6-eth1 s5-eth3:s7-eth1
s6 lo:  s6-eth1:s5-eth2 s6-eth2:h5-eth0 s6-eth3:h6-eth0
s7 lo:  s7-eth1:s5-eth3 s7-eth2:h7-eth0 s7-eth3:h8-eth0
c0
mininet> 

Ans 2:
Output of h7 ifconfig
mininet> h7 ifconfig
h7-eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.0.7  netmask 255.0.0.0  broadcast 10.255.255.255
        inet6 fe80::4c1e:4fff:fe9d:b37e  prefixlen 64  scopeid 0x20<link>
        ether 4e:1e:4f:9d:b3:7e  txqueuelen 1000  (Ethernet)
        RX packets 97  bytes 7786 (7.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 8  bytes 656 (656.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

Task 2:
Ans 1:
Function call graph:
start switch : _handle_PacketIn() -> act_like_hub() -> resend_packet() -> send(msg)

pkt flow: packet comes in -> _handle_PacketIn -> act_like_hub() or act_like_switch() ->  resend_packet() -> forward message to the port
	


Ans 2:
-- 10.0.0.2 ping statistics ---
100 packets transmitted, 100 received, 0% packet loss, time 99345ms
rtt min/avg/max/mdev = 2.487/5.671/8.181/1.113 ms

--- 10.0.0.8 ping statistics ---
100 packets transmitted, 100 received, 0% packet loss, time 99409ms
rtt min/avg/max/mdev = 8.104/19.944/32.075/3.298 ms

Ans 2a.
Average ping -  h1 and h2 - 5.671
Average ping - h1 and h8 - 19.944

Ans 2b. 
Minimum ping - h1 and h2 - 2.487
Minimum ping - h1 and h8 - 8.104
Maximum ping - h1 and h2 - 8.181
Maximum ping - h1 and h8 - 32.075

Ans 2c.
The ping between h1 and h2 is less because of seller no.of switches between them, whereas there are many switched between h1 and h8.

Ans 3.

Ans 3a. 
IPERF is a tool to mesure network performance and tuning.It supports tuning of various parameters like timing, buffers and protocols. It measures the throughput between any two nodes in a network line.

Ans 3b. 
mininet> iperf h1 h2
*** Iperf: testing TCP bandwidth between h1 and h2 
*** Results: ['4.18 Mbits/sec', '4.89 Mbits/sec']


mininet> iperf h1 h8
*** Iperf: testing TCP bandwidth between h1 and h8 
*** Results: ['2.08 Mbits/sec', '2.42 Mbits/sec']

Ans 3c.
The throughtput is higher between h1 and h2 that h and h8 because the lesser no. of switches between h1 and h2 and there are a lot of switches between h1 and h8. So a longer time is required to transfer the data from h1 to h8 than on h1 to h2. 

Ans 4.
By adding log.info("Switch observing traffic: %s" % (self.connection) in the line number 107 "of_tutorial" controller we can get the details, which help us to observe the traffic. Once we run the of_tutorial.py file we can observe that all switches receive traffic, and are flooded with packets as h1 to h8 is connected with switches.


Task 3:
Ans 1.
The code describes the action of building rules in OpenFlow controller attached to mininet. The act_like_switch function will be able to map or learn MAC address are located. If a MAC address is discovered and that is the destination address that the sourse sends to, the controller will have the capability to map the MAC address to port. This improves the performance by directing the packets to known ports. If the destination is not already known, it simply floods the packet to all destinations. MAC Learning Controller also helps to improve the ping times and throughputs as flooding happens less often.


Ans 2:
--- 10.0.0.2 ping statistics ---
100 packets transmitted, 100 received, 0% packet loss, time 99401ms
rtt min/avg/max/mdev = 2.019/6.536/11.952/1.508 ms

--- 10.0.0.8 ping statistics ---
100 packets transmitted, 100 received, 0% packet loss, time 99271ms
rtt min/avg/max/mdev = 8.165/20.872/27.802/2.781 ms

Ans 2a.
Average ping -  h1 and h2 - 6.3536
Average ping - h1 and h8 - 20.872

Ans 2b. 
Minimum ping - h1 and h2 - 2.019
Minimum ping - h1 and h8 - 8.165
Maximum ping - h1 and h2 - 11.952
Maximum ping - h1 and h8 - 27.802

Ans 2c.
The pings are quite faster in Task 2, than in switches. It was better when thay were acting as hubs. The maximum RTT for h1-h2 is larger as the controller is introducing the rule. The change was visible because of the controller was able to distinguish the port numbers and build the forwarding rules. 


Ans 3:
Ans 3a.
mininet> iperf h1 h2
*** Iperf: testing TCP bandwidth between h1 and h2 
*** Results: ['4.40 Mbits/sec', '5.36 Mbits/sec']

mininet> iperf h1 h8
*** Iperf: testing TCP bandwidth between h1 and h8 
*** Results: ['2.13 Mbits/sec', '2.59 Mbits/sec']

Ans 3b.
There is a change in the throughput between the Task 2 and Task 3 and its higher in Task 2. This is because of lesser network congestion in Task 3. Once all the port and switches learns the mac_to_port mapping then the port and switches will not be burdened much. 
