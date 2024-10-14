## Setting Interfaces IPs:

R1 config:

interface Gig0/0
ip address 172.16.1.1 255.255.255.0
no shutdown
exit

interface Se0/0/0
ip address 172.16.10.1 255.255.255.252
no shutdown
exit

interface Se0/0/1
ip address 172.16.10.9 255.255.255.252
no shutdown
exit

R2 config:

interface Gig0/0
ip address 172.16.2.1 255.255.255.0
no shutdown
exit

interface Se0/0/0
ip address 172.16.10.2 255.255.255.252
no shutdown
exit

interface Se0/0/1
ip address 172.16.10.5 255.255.255.252
no shutdown
exit

R3 config:

interface GigabitEthernet0/0
ip address 172.16.3.1 255.255.255.0
no shutdown
exit

interface GigabitEthernet0/1
ip address 172.16.6.1 255.255.255.0
no shutdown
exit

interface Se0/0/0
ip address 172.16.10.6 255.255.255.252
no shutdown
exit

interface Se0/0/1
ip address 172.16.10.17 255.255.255.252
no shutdown
exit

R4 config:

interface Gig0/0
ip address 172.16.4.1 255.255.255.0
no shutdown
exit

interface Se0/0/0
ip address 172.16.10.10 255.255.255.252
no shutdown
exit

interface Se0/0/1
ip address 172.16.10.13 255.255.255.252
no shutdown
exit

R5 config:

interface Gig0/0
ip address 172.16.5.1 255.255.255.0
no shutdown
exit

interface Se0/0/0
ip address 172.16.10.14 255.255.255.252
no shutdown
exit

interface Se0/0/1
ip address 172.16.10.18 255.255.255.252
no shutdown
exit

---

## Setting up RIPv2:

R1:
router rip
version 2
network 172.16.1.0
network 172.16.10.0
exit

R2:
router rip
version 2
network 172.16.2.0
network 172.16.10.0
exit

R3:
router rip
version 2
network 172.16.3.0
network 172.16.6.0
network 172.16.10.0
exit

R4:
router rip
version 2
network 172.16.4.0
network 172.16.10.0
exit

R5:
router rip
version 2
network 172.16.5.0
network 172.16.10.0
exit

---

## Setting up DHCP for R4:

ip dhcp excluded-address 172.16.4.1 172.16.4.10

ip dhcp pool PATIENTS
network 172.16.4.0 255.255.255.0
default-router 172.16.4.1
dns-server 8.8.8.8
lease 7
exit

show ip dhcp pool
show ip dhcp binding

show ip interface brief

---

## Setting up the Switches

### Switch1:
configure terminal
hostname Switch1

! Configure interfaces connected to R5 and other switches
interface FastEthernet0/1
description Connected to R5 Gig0/0
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/2
description Connected to Switch2 Fa0/1
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/3
description Connected to Switch2 Fa0/2
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/4
description Connected to Switch3 Fa0/1
switchport mode access
switchport access vlan 1
no shutdown
exit

! Save configuration
end
write memory

### Switch2:

configure terminal
hostname Switch2

! Configure interfaces connected to Switch1 and Switch3
interface FastEthernet0/1
description Connected to Switch1 Fa0/2
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/2
description Connected to Switch1 Fa0/3
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/3
description Connected to Switch3 Fa0/2
switchport mode access
switchport access vlan 1
no shutdown
exit

! Save configuration
end
write memory

### Switch3:

configure terminal
hostname Switch3

! Configure interfaces connected to Switch1, Switch2, and PC4
interface FastEthernet0/1
description Connected to Switch1 Fa0/4
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/2
description Connected to Switch2 Fa0/3
switchport mode access
switchport access vlan 1
no shutdown
exit

interface FastEthernet0/3
description Connected to PC4
switchport mode access
switchport access vlan 1
no shutdown
exit

! Save configuration
end
write memory

---

## Setting up the ACL config

### Router R1 (Front Desk):

access-list 100 deny ip any 172.16.2.0 0.0.0.255
access-list 100 deny ip any 172.16.3.0 0.0.0.255
access-list 100 deny ip any 172.16.5.0 0.0.0.255
access-list 100 permit tcp 172.16.1.0 0.0.0.255 172.16.4.0 0.0.0.255 eq www
access-list 100 permit ip 172.16.1.0 0.0.0.255 any
access-list 100 deny ip any any

interface Serial0/0/0
ip access-group 100 out
exit

interface Serial0/0/1
ip access-group 100 out
exit

### Router R2 (Doctor's Office):

access-list 110 deny ip any 172.16.2.0 0.0.0.255
access-list 110 permit ip any any

access-list 110 deny ip any 172.16.2.0 0.0.0.255
access-list 110 permit ip any any

### Router R3 (Nurse's Area):

access-list 120 permit ip 172.16.2.0 0.0.0.255 172.16.3.0 0.0.0.255
access-list 120 permit ip 172.16.2.0 0.0.0.255 172.16.6.0 0.0.0.255
access-list 120 deny ip any 172.16.3.0 0.0.0.255
access-list 120 deny ip any 172.16.6.0 0.0.0.255
access-list 120 permit ip any any

interface Serial0/0/0
ip access-group 120 in
exit

interface Serial0/0/1
ip access-group 120 in
exit

### Router R4 (Patient's Area):

access-list 130 deny ip 172.16.4.0 0.0.0.255 any
access-list 130 permit ip 172.16.4.0 0.0.0.255 any

access-list 131 permit tcp 172.16.1.0 0.0.0.255 172.16.4.0 0.0.0.255 eq www
access-list 131 deny ip 172.16.1.0 0.0.0.255 172.16.4.0 0.0.0.255
access-list 131 permit ip any any

interface Serial0/0/0
ip access-group 131 in
exit

interface Serial0/0/1
ip access-group 131 in
exit

interface GigabitEthernet0/0
ip access-group 130 out
exit

### Router R5 (Systems Administration):

access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.1.0 0.0.0.255
access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.2.0 0.0.0.255
access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.3.0 0.0.0.255
access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.6.0 0.0.0.255
access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.4.0 0.0.0.255
access-list 140 permit ip 172.16.5.0 0.0.0.255 172.16.7.0 0.0.0.255
access-list 140 deny ip any any

interface Serial0/0/0
ip access-group 140 out
exit

interface Serial0/0/1
ip access-group 140 out
exit











