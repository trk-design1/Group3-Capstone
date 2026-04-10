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
|Port  |Mode  |IP Address       |Connected to |Port(Connected device)|
|------|------|-----------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.131/24|Cloud        |T4.2
|G0/0/1|Manual|10.128.250.1/24  |Core-Switch1 |


ISP-Router2
|Port  |Mode  |IP Address      |Connected to |Port(Connected device)|
|------|------|-----------------|-------------|----------------------|
|G0/0/0|DHCP  |10.128.209.132/24|Cloud        |T4.1
|G0/0/1|Manual|10.128.250.2     |Core-Switch2 |





PROCEDURES

Step 1: Creating the logical and physical topology

The physical and logical topology where created stating the where each device is connected to, the ip address and the porrts in use.

Step 2: Building the physical server

The physical server was built with proxmox being installed inside. 

Step 3: Building the topology

The physical connections of our topology were connected.
