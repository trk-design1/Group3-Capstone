DOCUMENTATION OF XAVIER ACADEMY

DESCRIPTION

This is a documentation of Xavier Academy's network. This includes the logical and physical topologies, email communication, directory service, user accounts and a website.


REVERSION INFO
|Version|Date      |Description                                                              |Author      |
|-------|----------|-------------------------------------------------------------------------|------------|
|1.0    |07/04/2026|Description, reversion info, approval table, accountability matrix, Scope|Roman Peniel|
|1.1    |13/04/2026|Devices, services, addressing table, procedure step 1-2                  |Roman Peniel|
|1.2    |15/04/2026|Procedure step 3-4,  Security hardening, STP, SSH, banners,              |Roman Peniel|
|1.3    |16/04/2026|Procedure step 5-7, storm control, port security standards             |Roman Peniel|


APPROVAL TABLE
|Name     |Title  |Date      |
|---------|-------|----------|
|Mr. Felix|Teacher|07/04/2026|


SCOPE

This document applies to IT, Network and Systems Administrator, Staffs and the Director of the school.
This document is to be referred to and updated when:

a. Any new device or service is added

b. Any new device or service is removed

c. A new IT, Staff, System or Network Administrator is employed (so they understand the network of the school)

Objectives of this documentation are:
a. Have an updated documentation of the school

b. Train new staffs


ACCOUNTABILITY MATRIX
|Name           |Responsibility                                 |
|---------------|-----------------------------------------------|
|Roman Peniel   |SOP documentation,ADDS, DHCP and DNS           |
|Byansi Samora  |Logical topology and physical configuration    | 
|Ryle Camryn    |Physical Configuration and powerpoint          |
|Enakhano Zenith|Physical topology, logical topology and website|
|Sharma Dinesh  |Powerpoint and physical configuration          |

DEVICES

8 Desktop PC for students

5 Desktop PC for staff/IT/instructors

2 Layer 3 switches

4 Layer 2 Switches

2 Routers

1 Windows Server

3 Wireless Access Points


SERVICES

a. HTTPS

b. DNS

c. DHCP

d. Active Directory

NETWORK STANDARDS AND SECURITY BASELINE

1. Spanning Tree Protocol (STP)

To prevent switching loops and improve redundancy:

Rapid PVST+ shall be enabled.

Core Layer 3 switches shall be configured as root bridge
.
Secondary root bridge shall be configured on backup switch.

PortFast shall be enabled on end-user access ports only.

BPDU Guard shall be enabled on all user-facing ports.


Example:

spanning-tree mode rapid-pvst

spanning-tree vlan 1,10,20,30,40,50,88,99 root primary

spanning-tree portfast default

spanning-tree bpduguard default

2. Disable Discovery Protocols

To reduce information leakage:

no cdp run

no lldp run

3. Secure Shell (SSH)

Telnet is prohibited. SSH Version 2 shall be used.

hostname L3-S1

ip domain-name xavieracademy.local

crypto key generate rsa modulus 2048

ip ssh version 2

username admin secret StrongPassword

line vty 0 4

transport input ssh

login local

Access to management interfaces is restricted to VLAN 10 (IT/Management).

4. Login and Warning Banners

All network devices shall display authorized-use warnings.

banner motd #

WARNING: Authorized Xavier Academy Personnel Only.

Unauthorized access is prohibited and monitored.

#

5. Executive Timeouts

Idle sessions shall automatically disconnect.

Console


line console 0

exec-timeout 5 0

logging synchronous

VTY

line vty 0 4

exec-timeout 10 0

6. Storm Control

To protect against broadcast and multicast storms:

interface range fa0/1 - 24

storm-control broadcast level 5.00

storm-control multicast level 5.00

storm-control action shutdown

7. Unused Ports Security Standard

All unused ports shall be administratively disabled and assigned to an unused VLAN.

vlan 999

name UNUSED_PORTS

interface range fa0/10 - 24

switchport mode access

switchport access vlan 99

shutdown

description UNUSED PORT

8. Native VLAN for Untagged Traffic

Native VLAN shall be changed from default VLAN 1.

vlan 99

name Native

interface fa0/1

switchport trunk encapsulation dot1q

switchport mode trunk

switchport trunk native vlan 99


VLAN 1 shall not be used for user traffic.


ADDRESSING TABLE

DEVICE
ISP-Router1
|Port  |Mode  |IP Address       | Gateway      |Connected to |Port(Connected device)|
|------|------|-----------------|--------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.132/24|10.128.209.1  |Cloud        |T4.2                  |
|G0/0/1|Manual|192.168.100.1/24 |N/A           |L3-S1        |Fa/01                 |


ISP-Router2
|Port  |Mode  |IP Address       | Gateway      |Connected to |Port(Connected device)|
|------|------|-----------------|--------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.196/24|10.128.209.1  |Cloud        |T4.1                  |
|G0/0/1|Manual|192.168.60.1/24  |N/A           |L3-S2        |Fa/01                 |

VLAN TABLE
|VLAN|IP Address     |Name           |
|----|---------------|---------------| 
|20  |192.168.20.0/24|Classroom 1    |
|30  |192.168.30.0/24|Reception      |
|40  |192.168.40.0/24|Classroom 2    |
|99  |192.168.99.0/24|Native         |
|10  |192.168.10.0/24|IT/Management  |
|50  |192.168.50.0/24|Servers        |
|88  |192.168.88.0/24|Teachers       |

L3-S1
|Port   |IP Address        | Gateway      |Connected to |Port(Connected device)|VLAN|
|-------|------------------|--------------|-------------|----------------------|----|
|FA0/1  |192.168.100.2/24  |192.168.100.1 |ISP-Router1  |G0/0/1                |N/A |
|FA0/2  |192.168.20.1/24   |N/A           |L2-S1        |Fa0/1                 |20  |
|FA0/3  |192.168.30.1/24   |N/A           |L2-S2        |Fa0/1                 |30  |
|FA0/4  |192.168.40.1/24   |N/A           |L2-S3        |Fa0/1                 |40  |
|FA0/5  |192.168.99.1/24   |N/A           |L2-S4        |Fa0/2                 |99  |
|FA0/7  |192.168.88.1/24   |N/A           |ADDS Server  |NIC                   |88  |
|FA0/9  |192.168.10.1/24   |N/A           |L3-S2        |Fa0/9                 |N/A |
|FA0/10 |192.168.10.1/24   |N/A           |L3-S2        |Fa0/10                |N/A |

L3-S2
|Port   |IP Address        | Gateway      |Connected to |Port(Connected device)|VLAN|
|-------|------------------|--------------|-------------|----------------------|----|
|FA0/1  |192.168.60.14/24  |192.168.60.1  |ISP-Router2  |G0/0/1                |N/A |
|FA0/2  |192.168.100.15/24 |N/A           |L2-S1        |Fa0/2                 |20  |
|FA0/3  |192.168.30.1/24   |N/A           |L2-S2        |Fa0/2                 |30  |
|FA0/4  |192.168.40.1/24   |N/A           |L2-S3        |Fa0/2                 |40  |
|FA0/5  |192.168.99.1/24   |N/A           |L2-S4        |Fa0/1                 |99  |
|FA0/7  |192.168.88.1/24   |N/A           |ADDS Server  |NIC                   |88  |
|FA0/9  |192.168.10.1/24   |N/A           |L3-S2        |Fa0/9                 |N/A |
|FA0/10 |192.168.10.1/24   |N/A           |L3-S2        |Fa0/10                |N/A |

L2-S1-Classroom1
|Port                  |IP Address        | Gateway      |Connected to   |Port(Connected device)|VLAN|
|----------------------|------------------|--------------|---------------|----------------------|----|
|FA0/1                 |N/A               |192.168.100.1 |L3-S1          |Fa0/2                 |20  |
|FA0/2                 |N/A               |192.168.100.1 |L3-S2          |Fa0/2                 |20  |
|FA0/3                 |N/A               |192.168.100.1 |PC1(Classroom1)|NIC                   |N/A |
|FA0/19                |N/A               |192.168.100.1 |Xavier_AP1     |LAN 1                 |N/A |

L2-S2-Classroom2
|Port                  |IP Address        | Gateway      |Connected to   |Port(Connected device)|VLAN|
|----------------------|------------------|--------------|---------------|----------------------|----|
|FA0/1                 |N/A               |192.168.100.1 |L3-S1          |Fa0/3                 |20  |
|FA0/2                 |N/A               |192.168.100.1 |L3-S2          |Fa0/2                 |20  |
|FA0/3                 |N/A               |192.168.100.1 |PC2(Classroom2)|NIC                   |N/A |

L2-S3-Classroom3
|Port                  |IP Address        | Gateway      |Connected to   |Port(Connected device)|VLAN|
|----------------------|------------------|--------------|---------------|----------------------|----|
|FA0/1                 |N/A               |192.168.100.1 |L3-S1          |Fa0/4                 |20  |
|FA0/2                 |N/A               |192.168.100.1 |L3-S2          |Fa0/4                 |20  |
|FA0/3                 |N/A               |192.168.100.1 |PC3(Staff)     |NIC                   |N/A |


L2-S4-Classroom4
|Port                  |IP Address        | Gateway      |Connected to   |Port(Connected device)|VLAN|
|----------------------|------------------|--------------|---------------|----------------------|----|
|FA0/1                 |N/A               |192.168.100.1 |L3-S1          |Fa0/5                 |20  |
|FA0/2                 |N/A               |192.168.100.1 |L3-S2          |Fa0/5                 |20  |
|FA0/3                 |N/A               |192.168.100.1 |PC4(Reception) |NIC                   |N/A |


ACCESS CONTROL LISTS (ACL)

ISP-Router1

ip access-list extended EDGE_IN

 permit tcp any any 
 
 permit udp any any
 
 permit icmp any any echo-reply
 
 permit icmp any any unreachable
 
 permit icmp any any time-exceeded
 
 permit tcp any any eq 80

 permit tcp any any eq 443
 
 permit tcp 192.168.10.0 0.0.0.255 any eq 22
 
 deny   ip any any 

 ip access-list standard MGMT_SSH
 
 permit 192.168.10.0 0.0.0.255
 
 deny   any 
 

 ip access-list standard NAT_ACL
 
 permit 192.168.0.0 0.0.255.255
 

ISP-Router2

ip access-list standard NAT_ACL

 permit 192.168.0.0 0.0.255.255
 
 permit 172.16.0.0 0.0.255.255
 

 VTY Access: SSH from IT VLAN only
 
ip access-list standard MGMT_SSH

 permit 192.168.10.0 0.0.0.255
 
 deny   any log


L3-S1

ip access-list extended VLAN_POLICY

 permit icmp any any
 
 permit ospf any any
 
 permit udp any any
 
 permit tcp any any established
 
 permit tcp any any eq 80
 
 permit tcp any any eq 443
 
 permit tcp any any eq 53
 
 permit udp any any eq 53
 
 permit tcp 192.168.10.0 0.0.0.255 any eq 22
 
 deny   ip any any log
 

 ip access-list standard MGMT_SSH
 
 permit 192.168.10.0 0.0.0.255
 
 deny   any log
 


 L3-S2
 
ip access-list extended VLAN_POLICY

 permit icmp any any
 
 permit ospf any any
 
 permit udp any any
 
 permit tcp any any established
 
 permit tcp any any eq 80
 
 permit tcp any any eq 443
 
 permit tcp any any eq 53
 
 permit udp any any eq 53
 
 permit tcp 192.168.10.0 0.0.0.255 any eq 22
 
 deny   ip any any 
 

VTY Access: SSH from IT VLAN only

ip access-list standard MGMT_SSH

 permit 192.168.10.0 0.0.0.255
 
 deny   any log
 
 


PROCEDURES

Step 1: Design of Network Topology

Develop both logical and physical topology diagrams, clearly identifying device connections, IP addressing, and port assignments.

Step 2: Physical Server Deployment

Provision and configure the physical server hardware. Install the hypervisor (Proxmox VE) to support virtualization.

Step 3: Physical Network Setup

Establish all physical connections between routers, switches, servers, and end-user devices according to the topology design.

Step 4: IP Address Planning

Develop a structured IP addressing scheme for all network devices, ensuring consistency and scalability.

Step 5: Logical Configuration

Configure all devices within the simulated environment (e.g., Cisco Packet Tracer) to validate the network design.

Step 6: Deployment and Configuration

Implement the network physically by connecting and configuring all devices according to the validated design.

Step 7: Server Configuration

Install Windows Server 2022 on the virtual environment and configure the following services:

a. Active Directory Domain Services (AD DS)

b. DHCP (Dynamic Host Configuration Protocol)

c. DNS (Domain Name System)

Step 8: Website Development

Develop and deploy the Xavier Academy website to provide institutional information and services.
