# Basic-OSPF
This repository show the basic OSPF configuration between 2 routers .
You need to verify and troubleshoot with the below show commands and get the below output .


2#show ip protocols
-----------------------
*** IP Routing is NSF aware ***

Routing Protocol is "application"
  Sending updates every 0 seconds
  Invalid after 0 seconds, hold down 0, flushed after 0
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Maximum path: 32
  Routing for Networks:
  Routing Information Sources:
    Gateway         Distance      Last Update
  Distance: (default is 4)

Routing Protocol is "ospf 110"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 2.2.2.2
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
    10.0.12.2 0.0.0.0 area 0
    10.2.0.0 0.0.255.255 area 0
  Routing Information Sources:
    Gateway         Distance      Last Update
    1.1.1.1              110      00:30:59
  Distance: (default is 110)


R2#show ip ospf database
---------------------------

            OSPF Router with ID (2.2.2.2) (Process ID 110)

		Router Link States (Area 0)

Link ID         ADV Router      Age         Seq#       Checksum Link count
1.1.1.1         1.1.1.1         1883        0x80000004 0x004F2C 5
2.2.2.2         2.2.2.2         148         0x80000004 0x00A4AD 5

		Net Link States (Area 0)

Link ID         ADV Router      Age         Seq#       Checksum
10.0.12.1       1.1.1.1         1272        0x80000002 0x00CA4E
R2#show ip ospf rib

            OSPF Router with ID (2.2.2.2) (Process ID 110)


		Base Topology (MTID 0)

OSPF local RIB
Codes: * - Best, > - Installed in global RIB

*   10.0.12.0/29, Intra, cost 1, area 0, Connected
      via 10.0.12.2, GigabitEthernet0/0
*>  10.1.1.1/32, Intra, cost 2, area 0
      via 10.0.12.1, GigabitEthernet0/0
*>  10.1.2.1/32, Intra, cost 2, area 0
      via 10.0.12.1, GigabitEthernet0/0
*>  10.1.3.1/32, Intra, cost 2, area 0
      via 10.0.12.1, GigabitEthernet0/0
*>  10.1.4.1/32, Intra, cost 2, area 0
      via 10.0.12.1, GigabitEthernet0/0
*   10.2.7.2/32, Intra, cost 1, area 0, Connected
      via 10.2.7.2, Loopback0
*   10.2.8.2/32, Intra, cost 1, area 0, Connected
      via 10.2.8.2, Loopback1
*   10.2.9.2/32, Intra, cost 1, area 0, Connected
      via 10.2.9.2, Loopback2
*   10.2.10.2/32, Intra, cost 1, area 0, Connected
      via 10.2.10.2, Loopback3

  2#show ip ospf interface
--------------------------
Loopback0 is up, line protocol is up
  Internet Address 10.2.7.2/24, Area 0, Attached via Network Statement
  Process ID 110, Router ID 2.2.2.2, Network Type LOOPBACK, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Loopback interface is treated as a stub Host
Loopback1 is up, line protocol is up
  Internet Address 10.2.8.2/24, Area 0, Attached via Network Statement
  Process ID 110, Router ID 2.2.2.2, Network Type LOOPBACK, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Loopback interface is treated as a stub Host
Loopback2 is up, line protocol is up
  Internet Address 10.2.9.2/24, Area 0, Attached via Network Statement
  Process ID 110, Router ID 2.2.2.2, Network Type LOOPBACK, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Loopback interface is treated as a stub Host
Loopback3 is up, line protocol is up
  Internet Address 10.2.10.2/24, Area 0, Attached via Network Statement
  Process ID 110, Router ID 2.2.2.2, Network Type LOOPBACK, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Loopback interface is treated as a stub Host
GigabitEthernet0/0 is up, line protocol is up
  Internet Address 10.0.12.2/29, Area 0, Attached via Network Statement
  Process ID 110, Router ID 2.2.2.2, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Transmit Delay is 1 sec, State BDR, Priority 1
  Designated Router (ID) 1.1.1.1, Interface address 10.0.12.1
  Backup Designated router (ID) 2.2.2.2, Interface address 10.0.12.2
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:00
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/1/1, flood queue length 0
  Next 0x0(0)/0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 4 msec, maximum is 4 msec
  Neighbor Count is 1, Adjacent neighbor count is 1
    Adjacent with neighbor 1.1.1.1  (Designated Router)
  Suppress hello for 0 neighbor(s)

  
R2#show ip ospf interface br
----------------------------
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Lo0          110   0               10.2.7.2/24        1     LOOP  0/0
Lo1          110   0               10.2.8.2/24        1     LOOP  0/0
Lo2          110   0               10.2.9.2/24        1     LOOP  0/0
Lo3          110   0               10.2.10.2/24       1     LOOP  0/0
Gi0/0        110   0               10.0.12.2/29       1     BDR   1/1


R2#show ip ospf interface  brief
-------------------------------
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Lo0          110   0               10.2.7.2/24        1     LOOP  0/0
Lo1          110   0               10.2.8.2/24        1     LOOP  0/0
Lo2          110   0               10.2.9.2/24        1     LOOP  0/0
Lo3          110   0               10.2.10.2/24       1     LOOP  0/0
Gi0/0        110   0               10.0.12.2/29       1     BDR   1/1
R2#
