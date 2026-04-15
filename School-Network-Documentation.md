DOCUMENTATION OF XAVIER ACADEMY

DESCRIPTION

This is a documentation of Xavier Academy's network. This includes the logical and physical topologies, email communication, directory service, user accounts and a website.


REVERSION INFO
|Version|Date      |Description                                                              |Author      |
|-------|----------|-------------------------------------------------------------------------|------------|
|1.0    |07/04/2026|Description, reversion info, approval table, accountability matrix, Scope|Roman Peniel|
|1.1    |08/04/2026|Devices, services, addressing table, procedure step 1-2                  |Roman Peniel|


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
|Name           |Responsibility                        |
|---------------|--------------------------------------|
|Roman Peniel   |SOP documentation                     |
|Byansi Samora  |Logical topology                      | 
|Ryle Camryn    |Email communication and user accounts |
|Enakhano Zenith|Physical topology and Active Directory|
|Sharma Dinesh  |Logical topology                      |

DEVICES

8 Desktop PC for students

4 Laptop PC for Instructors

4 Desktop PC for staff

2 Desktop PC for IT

4 Switches

2 Routers

1 Windows Server

3 Wireless Access Points


SERVICES

a. HTTPS

b. DNS

c. DHCP

d. Active Directory


ADDRESSING TABLE
|Device     |Mode  |IP Adrress     |
|-----------|------|---------------|
|Router 1   |Manual|10.128.250.1/24|
|Router 2   |Manual|10.128.250.1/24|              
|Switch 1   |Manual|10.128.250.1/24|
|Switch 2   |Manual|10.128.250.1/24|
|Student PC1|DHCP  |10.128.250.1/24|
|Student PC2|DHCP  |10.128.250.1/24|
|Staff PC1  |DHCP  |10.128.250.1/24|
|IT PC      |DHCP  |10.128.250.1/24|
|Server     |Manual|10.128.250.1/24|

DEVICE
ISP-Router1
|Port  |Mode  |IP Address       | Gateway      |Connected to |Port(Connected device)|
|------|------|-----------------|--------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.131/24|10.128.209.1  |Cloud        |T4.2                  |
|G0/0/1|Manual|192.168.100.1/24 |N/A           |L3-S1        |Fa/01                 |


ISP-Router2
|Port  |Mode  |IP Address       | Gateway      |Connected to |Port(Connected device)|
|------|------|-----------------|--------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.131/24|10.128.209.1  |Cloud        |T4.1                  |
|G0/0/1|Manual|192.168.100.1/24 |N/A           |L3-S2        |Fa/03                 |

VLAN TABLE
|VLAN|IP Address     |Name           |
|----|---------------|---------------| 
|20  |192.168.20.0/24|Classroom 1    |
|30  |192.168.30.0/24|Reception      |
|40  |192.168.40.0/24|Classroom 2    |
|99  |192.168.99.0/24|Native         |
|10  |192.168.10.0/24|IT/Management  |
|88  |192.168.88.0/24|Teachers       |

L3-S1
|Port   |IP Address        | Gateway      |Connected to |Port(Connected device)|VLAN|
|-------|------------------|--------------|-------------|----------------------|----|
|FA0/1  |192.168.100.141/24|192.168.100.1 |ISP-Router1  |G0/0/1                |N/A |
|FA0/2  |192.168.20.1/24   |N/A           |SW-1         |Students-Class1 GW    |20  |
|FA0/3  |192.168.30.1/24   |N/A           |SW-1         |Students-Class1 GW    |30  |
|FA0/4  |192.168.40.1/24   |N/A           |SW-2         |Students-Class2 GW    |40  |
|FA0/5  |192.168.99.1/24   |N/A           |SW-2         |Students-Class1 GW    |99  |
|FA0/6  |192.168.88.1/24   |N/A           |SW-3         |Students-Class1 GW    |88  |
|FA0/9  |192.168.10.1/24   |N/A           |L3-S2        |Students-Class1 GW    |N/A |
|FA0/10 |192.168.10.1/24   |N/A           |L3-S2        |Students-Class1 GW    |N/A |

L3-S2
|Port   |IP Address        | Gateway      |Connected to |Port(Connected device)|VLAN|
|-------|------------------|--------------|-------------|----------------------|----|
|FA0/1  |192.168.100.141/24|192.168.100.1 |ADDS Server  |G0/0/1                |N/A |
|FA0/2  |192.168.100.15/24 |N/A           |ISP-Router2  |Students-Class1 GW    |20  |
|FA0/3  |192.168.30.1/24   |N/A           |SW-1         |Students-Class1 GW    |30  |
|FA0/4  |192.168.40.1/24   |N/A           |SW-2         |Students-Class2 GW    |40  |
|FA0/5  |192.168.99.1/24   |N/A           |SW-2         |Students-Class1 GW    |99  |
|FA0/6  |192.168.88.1/24   |N/A           |SW-3         |Students-Class1 GW    |88  |
|FA0/9  |192.168.10.1/24   |N/A           |L3-S2        |Students-Class1 GW    |N/A |
|FA0/10 |192.168.10.1/24   |N/A           |L3-S2        |Students-Class1 GW    |N/A |






PROCEDURES

Step 1: Creating the logical and physical topology

The physical and logical topology where created stating the where each device is connected to, the ip address and the porrts in use.

Step 2: Building the physical server

The physical server was built with proxmox being installed inside. 

Step 3: Building the topology

The physical connections of our topology were connected.

Step 4: Creating the Addressing Table

We created an addressing table for the routers, switches and pcs

Step 5: Configured the devices on the logical topology
We configured all the devices on the packet tracer 

Step 6: Connected the physical devices and configured them
We connected the routers, switches, servers and pcs according to the topology and configured them.

Step 7: Configuring the physical server
We installed proxmox on the physical server. Afterwards we installed Microsoft Server 2022 version on the  server. After the configuration we setup an Active Directory Domain Services (ADDS), Dynamic Host Configuration Protocol (DHCP) and Domain Name Service (DNS) on the server.

Step 8: Creation of the Website
The website was created featuring Xavier's Academy's information
