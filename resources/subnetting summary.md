# **1. LANs and Router Interfaces**

This table outlines each **Local Area Network (LAN)**, its **subnet**, the **connected router**, and the respective **router interface** with assigned IP addresses.

| **Department**           | **Subnet**      | **Router** | **Interface**      | **Router IP Address** | **Description**              |
|--------------------------|-----------------|------------|--------------------|-----------------------|------------------------------|
| **Front Desk**           | 172.16.1.0/24   | R1         | GigabitEthernet0/0 | 172.16.1.1            | Front Desk LAN               |
| **Doctor's Office**      | 172.16.2.0/24   | R2         | GigabitEthernet0/0 | 172.16.2.1            | Doctor's Office LAN          |
| **Nurse's Area (A)**     | 172.16.3.0/24   | R3         | GigabitEthernet0/0 | 172.16.3.1            | Nurse's Area LAN A           |
| **Nurse's Area (B)**     | 172.16.6.0/24   | R3         | GigabitEthernet0/1 | 172.16.6.1            | Nurse's Area LAN B           |
| **Patient's Area**       | 172.16.4.0/24   | R4         | GigabitEthernet0/0 | 172.16.4.1            | Patient's Area LAN           |
| **Systems Administration** | 172.16.5.0/24 | R5         | GigabitEthernet0/0 | 172.16.5.1            | Systems Administration LAN   |

---

## **2. WANs and Router Interfaces**

This table details each **Wide Area Network (WAN)** link, the **connected routers**, their respective **interfaces**, and the **assigned IP addresses** within their unique `/30` subnets.

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

---

## **3. PCs and Their IP Addresses**

This table lists each **PC**, the **connected router**, the **LAN subnet** it resides in, its **assigned IP address**, and the corresponding **default gateway**.

| **PC** | **Connected Router**   | **LAN Subnet**    | **Assigned IP Address** | **Subnet Mask**     | **Default Gateway** |
|--------|------------------------|-------------------|-------------------------|---------------------|---------------------|
| PC0    | R1 (Front Desk)        | 172.16.1.0/24     | 172.16.1.2              | 255.255.255.0 (/24) | 172.16.1.1          |
| PC1    | R2 (Doctor's Office)   | 172.16.2.0/24     | 172.16.2.2              | 255.255.255.0 (/24) | 172.16.2.1          |
| PC2    | R3 (Nurse's Area A)    | 172.16.3.0/24     | 172.16.3.2              | 255.255.255.0 (/24) | 172.16.3.1          |
| PC3    | R3 (Nurse's Area B)    | 172.16.6.0/24     | 172.16.6.2              | 255.255.255.0 (/24) | 172.16.6.1          |
| PC5    | R4 (Patient's Area)    | 172.16.4.0/24     | 172.16.4.2              | 255.255.255.0 (/24) | 172.16.4.1          |

---

## **4. Summary of Router Interface Configurations**

For quick reference, here's a consolidated view of all **Router Interfaces** with their assigned **IP addresses** and **subnets**.

### **Router R1**

| **Interface**    | **IP Address**   | **Subnet**        | **Description**      |
|------------------|------------------|--------------------|----------------------|
| GigabitEthernet0/0 | 172.16.1.1      | 172.16.1.0/24      | Front Desk LAN       |
| Serial0/0/0       | 172.16.10.1     | 172.16.10.0/30     | WAN1 to R2           |
| Serial0/0/1       | 172.16.10.9     | 172.16.10.8/30     | WAN3 to R4           |

### **Router R2**

| **Interface**    | **IP Address**   | **Subnet**        | **Description**       |
|------------------|------------------|--------------------|-----------------------|
| GigabitEthernet0/0 | 172.16.2.1      | 172.16.2.0/24      | Doctor's Office LAN   |
| Serial0/0/0       | 172.16.10.2     | 172.16.10.0/30     | WAN1 to R1            |
| Serial0/0/1       | 172.16.10.5     | 172.16.10.4/30     | WAN2 to R3            |

### **Router R3**

| **Interface**    | **IP Address**   | **Subnet**        | **Description**      |
|------------------|------------------|--------------------|----------------------|
| GigabitEthernet0/0 | 172.16.3.1      | 172.16.3.0/24      | Nurse's Area LAN A   |
| GigabitEthernet0/1 | 172.16.6.1      | 172.16.6.0/24      | Nurse's Area LAN B   |
| Serial0/0/0       | 172.16.10.6     | 172.16.10.4/30     | WAN2 to R2            |
| Serial0/0/1       | 172.16.10.17    | 172.16.10.16/30    | WAN5 to R5            |

### **Router R4**

| **Interface**    | **IP Address**   | **Subnet**        | **Description**        |
|------------------|------------------|--------------------|------------------------|
| GigabitEthernet0/0 | 172.16.4.1      | 172.16.4.0/24      | Patient's Area LAN     |
| Serial0/0/0       | 172.16.10.10    | 172.16.10.8/30     | WAN3 to R1             |
| Serial0/0/1       | 172.16.10.13    | 172.16.10.12/30    | WAN4 to R5             |

### **Router R5**

| **Interface**    | **IP Address**   | **Subnet**        | **Description**               |
|------------------|------------------|--------------------|-------------------------------|
| GigabitEthernet0/0 | 172.16.5.1      | 172.16.5.0/24      | Systems Administration LAN    |
| Serial0/0/0       | 172.16.10.14    | 172.16.10.12/30    | WAN4 to R4                     |
| Serial0/0/1       | 172.16.10.18    | 172.16.10.16/30    | WAN5 to R3                     |
