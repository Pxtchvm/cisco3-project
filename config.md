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

## Setting up OSPF:

R1:
router ospf 1
network 172.16.1.0 0.0.0.255 area 0
network 172.16.10.0 0.0.0.3 area 0
network 172.16.10.8 0.0.0.3 area 0
exit

router ospf 1
network 172.16.1.0 0.0.0.255 area 0
network 172.16.10.0 0.0.0.3 area 0
network 172.16.10.8 0.0.0.3 area 0


R2:
router ospf 1
network 172.16.4.0 0.0.0.255 area 0
network 172.16.10.8 0.0.0.3 area 0
network 172.16.10.12 0.0.0.3 area 0
exit

R3:
router ospf 1
network 172.16.3.0 0.0.0.255 area 0
network 172.16.6.0 0.0.0.255 area 0
network 172.16.10.4 0.0.0.3 area 0
network 172.16.10.16 0.0.0.3 area 0
exit

R4:
router ospf 1
network 172.16.4.0 0.0.0.255 area 0
network 172.16.10.8 0.0.0.3 area 0
network 172.16.10.12 0.0.0.3 area 0
exit

R5:
router ospf 1
network 172.16.5.0 0.0.0.255 area 0
network 172.16.10.12 0.0.0.3 area 0
network 172.16.10.16 0.0.0.3 area 0
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

















