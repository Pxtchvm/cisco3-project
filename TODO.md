## **1. Updated Network Summary Tables**

### **1.1. LANs, Switches, and Router Interfaces**

Here's an updated table that includes all **LANs**, **Switches**, **Router Interfaces**, and **PC IP Addresses** based on your expanded topology.

#### **LAN and Router Interface Summary**

| **Department**               | **Subnet**      | **Router** | **Interface**          | **Router IP Address** | **Description**              |
|------------------------------|-----------------|------------|------------------------|-----------------------|------------------------------|
| **Front Desk**               | 172.16.1.0/24   | R1         | GigabitEthernet0/0     | 172.16.1.1            | Front Desk LAN               |
| **Doctor's Office**          | 172.16.2.0/24   | R2         | GigabitEthernet0/0     | 172.16.2.1            | Doctor's Office LAN          |
| **Nurse's Area (A)**         | 172.16.3.0/24   | R3         | GigabitEthernet0/0     | 172.16.3.1            | Nurse's Area LAN A           |
| **Nurse's Area (B)**         | 172.16.6.0/24   | R3         | GigabitEthernet0/1     | 172.16.6.1            | Nurse's Area LAN B           |
| **Patient's Area**           | 172.16.4.0/24   | R4         | GigabitEthernet0/0     | 172.16.4.1            | Patient's Area LAN           |
| **Systems Administration**   | 172.16.5.0/24   | R5         | GigabitEthernet0/0     | 172.16.5.1            | Systems Admin LAN             |

#### **WAN Links and Router Interfaces**

| **WAN Link** | **Connected Routers** | **Subnet**      | **Subnet Mask**       | **Router** | **Interface**        | **IP Address**    |
|--------------|-----------------------|-----------------|-----------------------|------------|----------------------|--------------------|
| **WAN1**     | R1 ↔ R2               | 172.16.10.0/30  | 255.255.255.252 (/30) | R1         | Serial0/0/0          | 172.16.10.1        |
|              |                       |                 |                       | R2         | Serial0/0/0          | 172.16.10.2        |
| **WAN2**     | R2 ↔ R3               | 172.16.10.4/30  | 255.255.255.252 (/30) | R2         | Serial0/0/1          | 172.16.10.5        |
|              |                       |                 |                       | R3         | Serial0/0/0          | 172.16.10.6        |
| **WAN3**     | R1 ↔ R4               | 172.16.10.8/30  | 255.255.255.252 (/30) | R1         | Serial0/0/1          | 172.16.10.9        |
|              |                       |                 |                       | R4         | Serial0/0/0          | 172.16.10.10       |
| **WAN4**     | R4 ↔ R5               | 172.16.10.12/30 | 255.255.255.252 (/30) | R4         | Serial0/0/1          | 172.16.10.13       |
|              |                       |                 |                       | R5         | Serial0/0/0          | 172.16.10.14       |
| **WAN5**     | R3 ↔ R5               | 172.16.10.16/30 | 255.255.255.252 (/30) | R3         | Serial0/0/1          | 172.16.10.17       |
|              |                       |                 |                       | R5         | Serial0/0/1          | 172.16.10.18       |

#### **Switches and Their Connections**

| **Switch** | **Port** | **Connected Device** | **Device IP Address** | **Description**                             |
|------------|----------|----------------------|-----------------------|---------------------------------------------|
| **Switch1** | Fa0/1   | R5 (Gig0/0)           | 172.16.5.1             | Connection to R5 for Systems Admin LAN       |
|            | Fa0/2   | Switch2 (Fa0/1)        | N/A                   | Uplink to Switch2 via Fa0/1                  |
|            | Fa0/3   | Switch2 (Fa0/2)        | N/A                   | Uplink to Switch2 via Fa0/2                  |
|            | Fa0/4   | Switch3 (Fa0/1)        | N/A                   | Uplink to Switch3 via Fa0/1                  |
| **Switch2** | Fa0/1   | Switch1 (Fa0/2)        | N/A                   | Uplink from Switch1 via Fa0/2                 |
|            | Fa0/2   | Switch1 (Fa0/3)        | N/A                   | Uplink from Switch1 via Fa0/3                 |
|            | Fa0/3   | Switch3 (Fa0/2)        | N/A                   | Uplink to Switch3 via Fa0/2                    |
| **Switch3** | Fa0/1   | Switch1 (Fa0/4)        | N/A                   | Uplink from Switch1 via Fa0/4                 |
|            | Fa0/2   | Switch2 (Fa0/3)        | N/A                   | Uplink from Switch2 via Fa0/3                 |
|            | Fa0/3   | PC4                    | 172.16.x.x             | Connection to PC4                              |

> **Note:**
> - **Switch Ports Fa0/1, Fa0/2, etc.,** are connected to other switches or devices. These are **Layer 2 connections**, so no IP addresses are assigned to switch ports unless VLAN interfaces are configured (not covered here).
> - **PC4** will be detailed in the PC IP Addresses table.

#### **PCs and Their IP Addresses**

| **PC** | **Connected Switch** | **LAN Subnet**    | **Assigned IP Address** | **Subnet Mask**     | **Default Gateway** |
|--------|----------------------|-------------------|-------------------------|---------------------|---------------------|
| PC0    | Switch1 (connected to R1 via R1's LAN1) | 172.16.1.0/24     | 172.16.1.2              | 255.255.255.0 (/24) | 172.16.1.1          |
| PC1    | Switch1 (connected to R2 via R2's LAN2) | 172.16.2.0/24     | 172.16.2.2              | 255.255.255.0 (/24) | 172.16.2.1          |
| PC2    | Switch1 (connected to R3's LAN3a via R3) | 172.16.3.0/24     | 172.16.3.2              | 255.255.255.0 (/24) | 172.16.3.1          |
| PC3    | Switch1 (connected to R3's LAN3b via R3) | 172.16.6.0/24     | 172.16.6.2              | 255.255.255.0 (/24) | 172.16.6.1          |
| PC4    | Switch3              | 172.16.x.x        | Assigned via DHCP/Routing | 255.255.255.0 (/24) | 172.16.x.1 (Based on LAN) |
| PC5    | Switch1 (connected to R4's LAN4 via R4) | 172.16.4.0/24     | 172.16.4.2              | 255.255.255.0 (/24) | 172.16.4.1          |

> **Note:**
> - **PC4's** IP address will be assigned via **DHCP** or statically, depending on your configuration.
> - Ensure that **PC4**'s subnet and default gateway align with the **connected LAN**. Adjust `172.16.x.x` accordingly.

---

## **2. Understanding the Double Connections Between Switches**

### **2.1. Purpose of Redundant Links**

The **double connections** between **Switch1** and **Switch2** (i.e., Switch1's Fa0/2 to Switch2's Fa0/1 and Switch1's Fa0/3 to Switch2's Fa0/2) are typically implemented for the following reasons:

1. **Redundancy and Fault Tolerance:**
   - Provides **backup paths** in case one link fails, ensuring network resilience.
   
2. **Load Balancing:**
   - Distributes network traffic across multiple paths to optimize performance.

3. **Loop Prevention:**
   - Prevents network loops using **Spanning Tree Protocol (STP)**, which automatically blocks redundant paths to maintain a loop-free topology.

### **2.2. Implementing STP**

To prevent loops in networks with redundant connections, **STP** (or its variants like **RSTP**) is employed. STP automatically manages redundant paths by blocking one of them, only activating it if the primary path fails.

> **Recommendation:**
> - **Ensure STP is enabled** on all switches to handle redundant connections gracefully.
> - Verify **STP status** to confirm that redundant links are appropriately managed.

### **2.3. Verification of STP**

On **Cisco switches**, you can verify STP status using the following command:

```plaintext
Switch# show spanning-tree
```

**Expected Output:**
- Display of **STP root bridge**, **port roles**, and **blocked ports**.
- Confirm that one of the redundant links is **blocked** to prevent loops.

---

## **3. Configuring Routing Protocols (RIP and OSPFv2)**

Your network utilizes both **RIP** and **OSPFv2** for routing. While **OSPFv2** is more efficient for larger, hierarchical networks, **RIP** can be used for simpler, flat networks or specific routing segments as per your project requirements.

### **3.1. Deciding Between RIP and OSPFv2**

- **OSPFv2:**
  - **Pros:** Faster convergence, support for hierarchical routing (areas), more scalable.
  - **Cons:** More complex to configure.
  
- **RIP:**
  - **Pros:** Simpler to configure, easier to understand.
  - **Cons:** Slower convergence, limited scalability (max 15 hops), less efficient.

> **Recommendation:**
> - **Use OSPFv2** as the primary routing protocol for the entire network due to its scalability and efficiency.
> - **Implement RIP** only if specified by project requirements or for specific network segments.

### **3.2. Configuring OSPFv2 Across All Routers**

Assuming **OSPFv2** is the primary routing protocol, here's how to configure it on each router.

#### **3.2.1. OSPF Configuration Steps**

**For Each Router (R1 to R5):**

1. **Enter OSPF Router Configuration Mode:**

   ```plaintext
   Router(config)# router ospf 1
   ```

2. **Advertise Networks:**

   Use the `network` command with appropriate wildcard masks to include all relevant subnets.

   - **Syntax:**

     ```plaintext
     Router(config-router)# network [network-address] [wildcard-mask] area [area-id]
     ```

   - **Example for R1:**

     ```plaintext
     R1(config)# router ospf 1
     R1(config-router)# network 172.16.1.0 0.0.0.255 area 0
     R1(config-router)# network 172.16.10.0 0.0.0.3 area 0
     R1(config-router)# network 172.16.10.8 0.0.0.3 area 0
     R1(config-router)# exit
     ```

3. **Repeat for All Routers:**

   Ensure that each router advertises its **LAN subnets** and **WAN interfaces**.

#### **3.2.2. Complete OSPF Configuration for Each Router**

##### **Router R1**

```plaintext
R1(config)# router ospf 1
R1(config-router)# network 172.16.1.0 0.0.0.255 area 0
R1(config-router)# network 172.16.10.0 0.0.0.3 area 0
R1(config-router)# network 172.16.10.8 0.0.0.3 area 0
R1(config-router)# exit
```

##### **Router R2**

```plaintext
R2(config)# router ospf 1
R2(config-router)# network 172.16.2.0 0.0.0.255 area 0
R2(config-router)# network 172.16.10.0 0.0.0.3 area 0
R2(config-router)# network 172.16.10.4 0.0.0.3 area 0
R2(config-router)# exit
```

##### **Router R3**

```plaintext
R3(config)# router ospf 1
R3(config-router)# network 172.16.3.0 0.0.0.255 area 0
R3(config-router)# network 172.16.6.0 0.0.0.255 area 0
R3(config-router)# network 172.16.10.4 0.0.0.3 area 0
R3(config-router)# network 172.16.10.16 0.0.0.3 area 0
R3(config-router)# exit
```

##### **Router R4**

```plaintext
R4(config)# router ospf 1
R4(config-router)# network 172.16.4.0 0.0.0.255 area 0
R4(config-router)# network 172.16.10.8 0.0.0.3 area 0
R4(config-router)# network 172.16.10.12 0.0.0.3 area 0
R4(config-router)# exit
```

##### **Router R5**

```plaintext
R5(config)# router ospf 1
R5(config-router)# network 172.16.5.0 0.0.0.255 area 0
R5(config-router)# network 172.16.10.12 0.0.0.3 area 0
R5(config-router)# network 172.16.10.16 0.0.0.3 area 0
R5(config-router)# exit
```

#### **3.2.3. Verifying OSPF Configuration**

1. **Check OSPF Neighbors:**

   On each router, ensure that OSPF has formed neighbor relationships.

   ```plaintext
   Router# show ip ospf neighbor
   ```

   **Expected Output:**
   - Lists of **OSPF neighbors** with their **state** (should be "FULL").

2. **Check OSPF Routing Table:**

   Verify that all OSPF-learned routes are present.

   ```plaintext
   Router# show ip route ospf
   ```

   **Expected Output:**
   - Routes should be marked with an **"O"** indicating they are learned via OSPF.

3. **Check Overall Routing Table:**

   Ensure that all routes are properly populated.

   ```plaintext
   Router# show ip route
   ```

   **Expected Output:**
   - All **LAN** and **WAN** subnets should be present with correct next-hop information.

### **3.3. Configuring RIP (If Required)**

If your project requires **RIP** alongside **OSPFv2**, ensure it's correctly configured to avoid routing conflicts.

> **Note:** Running both **OSPFv2** and **RIP** can introduce complexities. Ensure they are configured to handle different parts of the network or use route filtering to prevent conflicts.

#### **RIP Configuration Example (Optional)**

**Router R1:**

```plaintext
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# network 172.16.1.0
R1(config-router)# network 172.16.10.0
R1(config-router)# exit
```

**Router R2:**

```plaintext
R2(config)# router rip
R2(config-router)# version 2
R2(config-router)# network 172.16.2.0
R2(config-router)# network 172.16.10.0
R2(config-router)# exit
```

**Router R3:**

```plaintext
R3(config)# router rip
R3(config-router)# version 2
R3(config-router)# network 172.16.3.0
R3(config-router)# network 172.16.6.0
R3(config-router)# network 172.16.10.0
R3(config-router)# exit
```

**Router R4:**

```plaintext
R4(config)# router rip
R4(config-router)# version 2
R4(config-router)# network 172.16.4.0
R4(config-router)# network 172.16.10.0
R4(config-router)# exit
```

**Router R5:**

```plaintext
R5(config)# router rip
R5(config-router)# version 2
R5(config-router)# network 172.16.5.0
R5(config-router)# network 172.16.10.0
R5(config-router)# exit
```

> **Caution:** Ensure that **OSPFv2** and **RIP** are not advertising the same networks unless intentionally designed. Use **route-maps** or **distribute lists** to control route advertisements if necessary.

---

## **4. Setting Up DHCPv4 for the Patient's Area (R4)**

To provide dynamic IP addressing to devices in the **Patient's Area (LAN4 - 172.16.4.0/24)**, configure **DHCPv4** on **Router R4**.

### **4.1. DHCP Configuration Steps on Router R4**

1. **Exclude Reserved IP Addresses:**

   Reserve IP addresses for the router and any static devices to prevent them from being assigned via DHCP.

   ```plaintext
   R4(config)# ip dhcp excluded-address 172.16.4.1 172.16.4.10
   ```

   > **Explanation:**
   > - **172.16.4.1** is the **default gateway** for the Patient's Area.
   > - **172.16.4.2** to **172.16.4.10** are excluded from DHCP assignment (adjust as needed).

2. **Create DHCP Pool:**

   Define a DHCP pool named **PATIENTS** for the Patient's Area.

   ```plaintext
   R4(config)# ip dhcp pool PATIENTS
   R4(dhcp-config)# network 172.16.4.0 255.255.255.0
   R4(dhcp-config)# default-router 172.16.4.1
   R4(dhcp-config)# dns-server 8.8.8.8
   R4(dhcp-config)# lease 7
   R4(dhcp-config)# exit
   ```

   > **Explanation:**
   > - **network:** Defines the DHCP pool's subnet.
   > - **default-router:** Specifies the default gateway for DHCP clients.
   > - **dns-server:** Specifies the DNS server IP address (Google's DNS used here).
   > - **lease:** Sets the lease duration in days (adjust as needed).

3. **Verify DHCP Configuration:**

   ```plaintext
   R4# show ip dhcp pool
   ```

   ```plaintext
   R4# show ip dhcp binding
   ```

   > **Expected Output:**
   > - **DHCP pool PATIENTS** details.
   > - **Assigned IP addresses** to connected devices.

4. **Ensure Interface is Up:**

   Verify that **GigabitEthernet0/0** on **R4** is up and correctly configured.

   ```plaintext
   R4# show ip interface brief
   ```

   **Expected Output:**

   ```
   Interface              IP-Address      OK? Method Status                Protocol
   GigabitEthernet0/0     172.16.4.1      YES manual up                    up
   Serial0/0/0            172.16.10.10     YES manual up                    up
   Serial0/0/1            172.16.10.13    YES manual up                    up
   ```

### **4.2. Assigning IP Addresses to PC4**

Assuming **PC4** is connected to **Switch3 (Fa0/3)**, ensure it receives an IP address via DHCP or assign it statically.

1. **DHCP Assigned IP (Preferred):**

   - **On PC4:**
     - Set IP configuration to **Obtain an IP address automatically**.
     - PC4 should receive an IP within the **172.16.4.0/24** subnet, e.g., **172.16.4.11**.

2. **Static IP Assignment (Alternative):**

   - **On PC4:**
     - **IP Address:** 172.16.4.11
     - **Subnet Mask:** 255.255.255.0
     - **Default Gateway:** 172.16.4.1
     - **DNS Server:** 8.8.8.8

> **Recommendation:**
> - **Use DHCP** for dynamic IP assignment to simplify management, especially if multiple devices will connect to the Patient's Area.
> - **Reserve static IPs** for essential devices (servers, printers) within the DHCP excluded range.

---

## **5. Verifying and Troubleshooting Connectivity**

After configuring **Routing** and **DHCP**, perform comprehensive verification to ensure all network components communicate as intended.

### **5.1. Ping Tests**

1. **From Each PC:**

   - **Ping Default Gateway:**
     - **PC0:** `ping 172.16.1.1`
     - **PC1:** `ping 172.16.2.1`
     - **PC2:** `ping 172.16.3.1`
     - **PC3:** `ping 172.16.6.1`
     - **PC4:** `ping 172.16.4.1`
     - **PC5:** `ping 172.16.4.1`

   - **Ping Other PCs:**
     - **From PC0 to PC1:** `ping 172.16.2.2`
     - **From PC1 to PC0:** `ping 172.16.1.2`
     - **From PC4 to PC1:** `ping 172.16.2.2`

2. **From Routers:**

   - **Ping Connected Interfaces:**
     - **From R1:** `ping 172.16.10.2` (R2's WAN1)
     - **From R2:** `ping 172.16.10.1` (R1's WAN1)
     - **From R3:** `ping 172.16.10.2` (R2's WAN1)
     - **From R4:** `ping 172.16.10.1` (R1's WAN1)
     - **From R5:** `ping 172.16.10.1` (R1's WAN1)
   
   - **Ping Other Router Interfaces:**
     - Ensure that all **WAN links** are operational by pinging respective interfaces.

### **5.2. Verify Routing Tables**

1. **On Each Router:**

   ```plaintext
   Router# show ip route
   ```

   **Expected Output:**
   - All **LAN** and **WAN** subnets should be present with correct **next-hop** information.
   - **OSPF** learned routes should be indicated with an **"O"**.

### **5.3. Verify OSPF Neighbors**

1. **On Each Router:**

   ```plaintext
   Router# show ip ospf neighbor
   ```

   **Expected Output:**
   - List of **OSPF neighbors** with their **states** (should be "FULL").

### **5.4. Verify DHCP Assignments**

1. **On PC4:**

   - Check if it has received a valid **IP address** via DHCP.
   - Use the command:

     ```plaintext
     ipconfig /all
     ```

     or

     ```plaintext
     ifconfig
     ```

     depending on your operating system.

   **Expected Output:**
   - **IP Address:** Within **172.16.4.0/24** (e.g., **172.16.4.11**)
   - **Default Gateway:** **172.16.4.1**
   - **DNS Server:** **8.8.8.8**

### **5.5. Inspect Access Control Lists (ACLs)**

Ensure that **ACLs** are not inadvertently blocking essential traffic.

1. **On Each Router:**

   ```plaintext
   Router# show access-lists
   ```

   **Review:**
   - **Permitted and Denied Traffic** as per your project requirements.
   - Ensure **ACLs** reference the **correct subnets**.

2. **Adjust ACLs If Necessary:**

   - **Example for Router R1:**

     ```plaintext
     R1(config)# access-list 100 permit ip 172.16.1.0 0.0.0.255 172.16.4.0 0.0.0.255 eq www
     R1(config)# access-list 100 deny ip any 172.16.2.0 0.0.0.255
     R1(config)# access-list 100 deny ip any 172.16.3.0 0.0.0.255
     R1(config)# access-list 100 deny ip any 172.16.5.0 0.0.0.255
     R1(config)# access-list 100 permit ip any any
     ```

   - **Apply ACL to Relevant Interfaces:**

     ```plaintext
     R1(config)# interface Serial0/0/0
     R1(config-if)# ip access-group 100 out
     R1(config-if)# exit
     
     R1(config)# interface Serial0/0/1
     R1(config-if)# ip access-group 100 out
     R1(config-if)# exit
     ```

   > **Note:** Adjust ACL numbers and rules based on your specific requirements and updated subnetting.

### **5.6. Verify Spanning Tree Protocol (STP) on Switches**

Ensure that **STP** is functioning correctly to manage redundant links.

1. **On Each Switch:**

   ```plaintext
   Switch# show spanning-tree
   ```

   **Expected Output:**
   - **Root Bridge:** One switch should be the root.
   - **Port Roles:** Root ports, designated ports, and blocked ports.
   - **No Loops:** Confirm that redundant links are appropriately blocked.

---

## **6. Addressing the Current Ping Issue**

Your current ping attempt to **PC1 (172.16.2.2)** from **PC0 (172.16.1.2)** resulted in "Destination host unreachable." Here's a step-by-step approach to troubleshoot and resolve this issue.

### **6.1. Verify Physical Connectivity**

1. **Check Cable Connections:**
   - Ensure that all cables are properly connected between devices, switches, and routers.
   - Verify that **PC1** is connected to **Switch1** and **Switch1** is connected to **R2**'s LAN interface.

2. **Check Interface Status:**
   - On **R1** and **R2**, ensure that **all interfaces** are **up/up**.

   ```plaintext
   Router# show ip interface brief
   ```

   **Expected Output:**
   - All interfaces should show **"up/up"** status.

### **6.2. Verify IP Configuration on PC1**

1. **On PC1:**

   - Ensure the following settings:

     - **IP Address:** 172.16.2.2
     - **Subnet Mask:** 255.255.255.0
     - **Default Gateway:** 172.16.2.1
     - **DNS Server:** As configured (e.g., 8.8.8.8)

2. **Check IP Assignment:**

   - If using **static IP**, confirm manual settings.
   - If using **DHCP**, ensure that **R2** (or the relevant router) is configured to provide DHCP (if applicable).

### **6.3. Verify Router R2's Configuration**

1. **Check IP Addressing:**

   ```plaintext
   R2# show running-config interface GigabitEthernet0/0
   ```

   **Expected Output:**

   ```plaintext
   interface GigabitEthernet0/0
    ip address 172.16.2.1 255.255.255.0
    no shutdown
   ```

2. **Check Routing Table:**

   ```plaintext
   R2# show ip route
   ```

   **Expected Output:**
   - **172.16.1.0/24** via **WAN1** (Serial0/0/0)
   - **Other LANs and WANs** as per OSPF/RIP configuration.

3. **Ping from R2 to PC1:**

   ```plaintext
   R2# ping 172.16.2.2
   ```

   **Expected Output:**
   - **Success:** Replies from PC1.

   > **If Ping Fails:** Check PC1's connectivity and IP settings.

### **6.4. Verify Routing Between R1 and R2**

1. **On Router R1:**

   - **Ping R2's LAN Interface:**

     ```plaintext
     R1# ping 172.16.2.1
     ```

     **Expected Output:**
     - **Success:** Replies from 172.16.2.1.

   - **If Ping Fails:**
     - Check **WAN1** link (Serial0/0/0 between R1 and R2).
     - Verify OSPF neighbor relationship on **R1** and **R2**.

2. **On Router R2:**

   - **Ping R1's LAN Interface:**

     ```plaintext
     R2# ping 172.16.1.1
     ```

     **Expected Output:**
     - **Success:** Replies from 172.16.1.1.

   - **If Ping Fails:**
     - Check **WAN1** link.
     - Verify OSPF neighbor relationship.

### **6.5. Review Access Control Lists (ACLs)**

1. **On Router R2:**

   - **ACL 10** was configured to **deny** access to the Doctor's Office network.

     ```plaintext
     access-list 10 deny any 172.16.2.0 0.0.0.255
     access-list 10 permit any
     ```

   - **Apply ACL to Incoming WAN Interfaces:**

     ```plaintext
     interface Serial0/0/0
      ip access-group 10 in

     interface Serial0/0/1
      ip access-group 10 in
     ```

2. **Impact of ACL on R2:**

   - **ACL 10** **denies** any traffic destined **to** **172.16.2.0/24** **from any source**.
   - This means that **external devices** cannot access the Doctor's Office network, which aligns with your project requirements.
   - **However, ensure that internal traffic from **R2** to **PC1** is not blocked.

3. **Solution:**

   - **ACLs on R2** should **only** restrict **incoming** traffic **from external sources**.
   - Ensure that **R2** can still route **internal traffic** to **PC1** without restrictions.

   > **Check Internal Routing:**
   > - **PC1** should be able to communicate within its subnet without ACL restrictions.

### **6.6. Adjust ACLs If Necessary**

1. **On Router R2:**

   - **Modify ACL 10** to **allow** internal traffic while restricting external access.

   ```plaintext
   R2(config)# access-list 10 deny ip any 172.16.2.0 0.0.0.255
   R2(config)# access-list 10 permit ip 172.16.2.0 0.0.0.255
   R2(config)# access-list 10 permit ip any any
   ```

   > **Explanation:**
   > - **Deny** any traffic **from external sources** to **172.16.2.0/24**.
   > - **Permit** traffic **within** **172.16.2.0/24**.
   > - **Permit** all other traffic.

2. **Reapply ACL:**

   ```plaintext
   R2(config)# interface Serial0/0/0
   R2(config-if)# ip access-group 10 in
   R2(config-if)# exit

   R2(config)# interface Serial0/0/1
   R2(config-if)# ip access-group 10 in
   R2(config-if)# exit
   ```

3. **Test Connectivity:**

   - **From PC0 (Front Desk) to PC1 (Doctor's Office):**

     ```plaintext
     PC0> ping 172.16.2.2
     ```

   - **Expected Output:**
     - **Success:** Replies from PC1.

   - **If Still Unreachable:**
     - Re-examine **ACL rules** to ensure they permit necessary traffic.
     - **Ensure OSPF** is correctly routing traffic between subnets.

---

## **7. Final Verification and Testing**

After implementing the above configurations and adjustments, perform a comprehensive verification to ensure network functionality.

### **7.1. Verify OSPF Neighbors and Routes**

1. **On Each Router:**

   ```plaintext
   Router# show ip ospf neighbor
   Router# show ip route ospf
   ```

   **Expected Output:**
   - **Full Adjacency:** All OSPF neighbors should be in the **"FULL"** state.
   - **Routing Table:** All **LAN** and **WAN** subnets should be present and reachable.

### **7.2. Verify DHCP Functionality**

1. **On PC4:**

   - **Obtain IP Address:**

     ```plaintext
     PC4> ipconfig /renew
     ```

   - **Check Assigned IP:**

     ```plaintext
     PC4> ipconfig
     ```

   **Expected Output:**
   - **IP Address:** Within **172.16.4.0/24** (e.g., **172.16.4.11**)
   - **Default Gateway:** **172.16.4.1**
   - **DNS Server:** **8.8.8.8**

### **7.3. Perform Connectivity Tests**

1. **From PC0 (Front Desk):**

   - **Ping PC1 (Doctor's Office):**

     ```plaintext
     PC0> ping 172.16.2.2
     ```

   - **Expected Output:**
     - **Success:** Replies from 172.16.2.2.

2. **From PC1 (Doctor's Office):**

   - **Ping PC0 (Front Desk):**

     ```plaintext
     PC1> ping 172.16.1.2
     ```

   - **Expected Output:**
     - **Success:** Replies from 172.16.1.2.

3. **From PC4 (Patient's Area):**

   - **Ping Default Gateway:**

     ```plaintext
     PC4> ping 172.16.4.1
     ```

   - **Ping Other PCs:**

     ```plaintext
     PC4> ping 172.16.1.2
     PC4> ping 172.16.2.2
     ```

   - **Expected Output:**
     - **Depends on ACLs:** As per project requirements, **Patient's Area** should not access other departments except specific services.

### **7.4. Verify ACL Functionality**

Ensure that **Access Control Lists** are enforcing your specified policies.

1. **Example Policy Checks:**

   - **Doctor’s Office (R2)** cannot be accessed by **anyone** except **the Doctor's Office itself**.
     - **From PC0:** `ping 172.16.2.2` → **Should Succeed** (if internal)
     - **From external sources:** `ping 172.16.2.2` → **Should Fail**

   - **Nurse's Area (R3)** can **only be accessed** by **Doctors**.
     - **From Doctor's Office:** `ping 172.16.3.1` → **Should Succeed**
     - **From Patient's Area:** `ping 172.16.3.1` → **Should Fail**

   - **Front Desk (R1)** can access **Patient’s Area (R4)** only for **payment status** (e.g., HTTP traffic).

2. **Testing ACLs:**

   - Use **ping** to test ICMP traffic.
   - Use **telnet** or **HTTP clients** to test specific service access (e.g., HTTP on port 80).

3. **Review ACL Logs (If Logging is Enabled):**

   - **On Each Router:**

     ```plaintext
     Router# show access-lists
     Router# show logging
     ```

   - **Analyze Logs:** Look for **denied** or **permitted** traffic as per ACL rules.

### **7.5. Monitor Spanning Tree Protocol (STP)**

Ensure that **STP** is preventing network loops due to redundant switch connections.

1. **On Each Switch:**

   ```plaintext
   Switch# show spanning-tree
   ```

   **Expected Output:**
   - **Root Bridge:** Only one switch should be the root.
   - **Port Roles:** Verify that redundant links are in the **blocked** state.
   - **No Loops:** Confirm that there are no active loops in the network.

### **7.6. Addressing Remaining Issues**

If after all configurations, connectivity issues persist:

1. **Re-examine ACL Rules:**

   - Ensure that **ACLs** are not overly restrictive.
   - Verify that **ACLs** allow necessary routing protocol traffic (e.g., OSPF).

2. **Check Routing Protocols:**

   - Ensure that **OSPF** is correctly advertising all necessary subnets.
   - Verify that **OSPF neighbors** are established and routes are learned.

3. **Verify Interface Configurations:**

   - Ensure that **all interfaces** are correctly configured with **IP addresses** and **subnet masks**.
   - Confirm that **interfaces are not in shutdown** state.

4. **Consult Router Logs:**

   - Look for any **error messages** or **warnings** related to routing, ACLs, or interface issues.

   ```plaintext
   Router# show logging
   ```

---

## **8. Summary of Configurations**

### **8.1. LAN Subnets**

- **Front Desk (R1 - LAN1):** `172.16.1.0/24`
- **Doctor's Office (R2 - LAN2):** `172.16.2.0/24`
- **Nurse's Area (R3 - LAN3a & LAN3b):** `172.16.3.0/24` and `172.16.6.0/24`
- **Patient's Area (R4 - LAN4):** `172.16.4.0/24`
- **Systems Administration (R5 - LAN5):** `172.16.5.0/24`

### **8.2. WAN Subnets**

- **WAN1 (R1 ↔ R2):** `172.16.10.0/30`
- **WAN2 (R2 ↔ R3):** `172.16.10.4/30`
- **WAN3 (R1 ↔ R4):** `172.16.10.8/30`
- **WAN4 (R4 ↔ R5):** `172.16.10.12/30`
- **WAN5 (R3 ↔ R5):** `172.16.10.16/30`

### **8.3. Switch Connections**

- **Switch1:**
  - **Fa0/1:** Connected to **R5 (Gig0/0)**
  - **Fa0/2:** Connected to **Switch2 (Fa0/1)**
  - **Fa0/3:** Connected to **Switch2 (Fa0/2)**
  - **Fa0/4:** Connected to **Switch3 (Fa0/1)**
  
- **Switch2:**
  - **Fa0/1:** Connected to **Switch1 (Fa0/2)**
  - **Fa0/2:** Connected to **Switch1 (Fa0/3)**
  - **Fa0/3:** Connected to **Switch3 (Fa0/2)**
  
- **Switch3:**
  - **Fa0/1:** Connected to **Switch1 (Fa0/4)**
  - **Fa0/2:** Connected to **Switch2 (Fa0/3)**
  - **Fa0/3:** Connected to **PC4**

### **8.4. PC IP Assignments**

| **PC** | **Connected Switch** | **LAN Subnet**    | **Assigned IP Address** | **Subnet Mask**     | **Default Gateway** |
|--------|----------------------|-------------------|-------------------------|---------------------|---------------------|
| PC0    | Switch1              | 172.16.1.0/24     | 172.16.1.2              | 255.255.255.0 (/24) | 172.16.1.1          |
| PC1    | Switch1              | 172.16.2.0/24     | 172.16.2.2              | 255.255.255.0 (/24) | 172.16.2.1          |
| PC2    | Switch1              | 172.16.3.0/24     | 172.16.3.2              | 255.255.255.0 (/24) | 172.16.3.1          |
| PC3    | Switch1              | 172.16.6.0/24     | 172.16.6.2              | 255.255.255.0 (/24) | 172.16.6.1          |
| PC4    | Switch3              | 172.16.4.0/24     | 172.16.4.11 (via DHCP)  | 255.255.255.0 (/24) | 172.16.4.1          |
| PC5    | Switch1              | 172.16.4.0/24     | 172.16.4.2              | 255.255.255.0 (/24) | 172.16.4.1          |

---

## **9. Additional Recommendations**

### **9.1. Documentation**

- **Maintain Updated Diagrams:**
  - Use tools like **Cisco Packet Tracer**, **Visio**, or **Lucidchart** to create and update network diagrams.
  
- **Configuration Backups:**
  - Regularly **backup** router and switch configurations.
  
- **Change Management:**
  - Document all changes made to the network for future reference and troubleshooting.

### **9.2. Security Enhancements**

- **Secure Router Access:**
  - Implement **SSH** for secure remote management.
  - Use **strong passwords** and **enable encryption** where possible.

- **Implement Firewalls:**
  - Consider **firewall rules** for enhanced security beyond ACLs.

- **Regular Updates:**
  - Keep all devices' firmware and software **up to date** to protect against vulnerabilities.

### **9.3. Network Monitoring**

- **Enable Logging:**
  - Configure **Syslog** servers to collect logs from routers and switches.
  
- **Use Network Monitoring Tools:**
  - Tools like **SolarWinds**, **Nagios**, or **PRTG** can help monitor network health and performance.

### **9.4. Redundancy and High Availability**

- **Additional Redundancy:**
  - If needed, implement **redundant routers** or **links** to ensure network availability.

- **Load Balancing:**
  - Distribute traffic across multiple paths to optimize performance.

### **9.5. Future Scalability**

- **Plan for Growth:**
  - Ensure that the IP addressing scheme and network design can accommodate future expansion.
  
- **VLAN Implementation:**
  - Consider implementing **VLANs** for better traffic management and security segmentation.

---

## **10. Conclusion**

By incorporating the switches into your network design and ensuring proper routing and DHCP configurations, you've established a robust and scalable network for your clinic. Here's a recap of the key steps taken:

1. **Updated Network Documentation:** Included switches and PC4, ensuring a comprehensive overview of the network topology.
2. **Understanding Redundant Links:** Implemented double connections between switches for redundancy, managed by Spanning Tree Protocol (STP).
3. **Configured Routing Protocols:** Set up **OSPFv2** across all routers to handle dynamic routing efficiently.
4. **Set Up DHCPv4:** Enabled DHCP on **Router R4** for the Patient's Area to provide dynamic IP addressing.
5. **Verification and Troubleshooting:** Performed ping tests, verified OSPF neighbors, and ensured ACLs are correctly enforcing access policies.

### **Next Steps:**

1. **Finalize ACL Configurations:**
   - Ensure that **ACLs** are precisely enforcing your access control requirements without hindering necessary traffic.

2. **Continuous Testing:**
   - Regularly perform connectivity tests to ensure all network components communicate as intended.
   
3. **Monitor Network Health:**
   - Implement monitoring solutions to track network performance and identify issues proactively.

4. **Enhance Security Measures:**
   - Beyond ACLs, implement additional security protocols to safeguard your network.

5. **Documentation and Training:**
   - Document all configurations and provide training to relevant personnel for network management and troubleshooting.