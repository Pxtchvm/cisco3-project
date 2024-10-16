I have a CISCO project that's the following:

# **Cisco 3 Network Design**

### **Project for ITS163L: Advanced Computer Network 1**

### **Project Description:**

Design an **ACL network** for a **clinic** with the following specifications:

1. **Router R1** – Front Desk network (`172.16.1.0/16`)
2. **Router R2** – Doctor's Office network (`172.16.2.0/16`)
3. **Router R3** – Nurse's Area network (`172.16.3.0/16`)
4. **Router R4** – Patient's Area network (`172.16.4.0/16`)
5. **Router R5** – Systems Administration network (`172.16.5.0/16`)

---

### **Access Control List (ACL) Conditions:**

1. **Doctor’s Office (R2)** cannot be accessed by **anyone**.
2. **Nurse's Area (R3)** can **only be accessed** by **doctors**.
3. **Front Desk (R1)** network can be accessed by both **nurses** and **doctors**.
4. **Patient’s Area (R4)** cannot access any other department.
5. **Front Desk (R1)** can only access the **Patient’s Area (R4)** to check **payment status**.

---

### **Additional Network Specifications:**

- **DHCPv4** is enabled in the **Patient's Area (R4)**.
- **RIP** is used for the rest of the network.
- **OSPFv2** is applied across the **entire network**.

Basically the topology is as follows:

Router 1 (R1):
connected to WAN1 through Se0/0/0
connected to WAN3 through Se0/0/1
connected to LAN1 through Gig0/0 (Front Desk network)

Router 2 (R2):
connected to WAN1 through Se0/0/0
connected to WAN2 through Se0/0/1
connected to LAN2 through Gig0/0  (Doctor's Office network)

Router 3 (R3):
connected to WAN2 through Se0/0/0
connected to WAN5 through Se0/0/1
connected to LAN3a through Gig0/0 (Nurse's Area network)
connected to LAN3b through Gig0/1 (Nurse's Area network)

Router 4 (R4):
connected to WAN3 through Se0/0/0
connected to WAN4 through Se0/0/1
connected to LAN4 through Gig0/0 (Patient's Area network)

Router 5 (R5):
connected to WAN4 through Se0/0/0
connected to WAN5 through Se0/0/1
connected to LAN3a through Gig0/0 (Systems Administration network)

PC0:
connected to LAN1

PC1:
connected to LAN2

PC2:
connected to LAN3a

PC3:
connected to LAN3b

PC5:
connected to LAN4

R5 is connected to Switch1 (Fa0/1) through Gig0/0

Switch1:
Connected to Switch2 through Fa0/2 and Fa0/3 (Fa0/2 is connected to Switch2's Fa0/1 and Fa0/3 is connected to Switch2's Fa0/2)
Connected to Switch3 through Fa0/4

Switch2:
Connected to Switch1 through Fa0/1 and Fa0/2 (Fa0/1 is connected to Switch1's Fa0/2 and Fa0/2 is connected to Switch1's Fa0/3)
Connected to Switch3 through Fa0/3

Switch3:
Connected to Switch1 through Fa0/1
Connected to Switch2 through Fa0/2
Connected to PC4 through Fa0/3

PC4 is connected to Switch3













