# **Cisco 3 Network Design**

### **Project for ITS163L: Advanced Computer Network 1**

---

### **Members:**

- Chua, Aaron  
- De Chavez, Paolo  
- Duldulao, Jacob  
- Espeno, John  
- Estaris, Aaron  
- Ilagan, Kirk  
- Ong, Anton  
- Pantalla, Sean  
- Pua, Richard  
- Rada, Julian  
- Sargento, Maxine  
- Villar, Sean  

---

### **Deadline:**
- **November 14, 2024, 9:15 PM** for 100% working design

### **Duration:**
- Progress is to be submitted **every class**.
- **End of class** progress reports must be submitted to the instructor.

---

### **Grading Criteria:**
- **Working** – 100 pts
- **Partial Working** – 50 pts

---

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

---

mwlb: Pxtchvm