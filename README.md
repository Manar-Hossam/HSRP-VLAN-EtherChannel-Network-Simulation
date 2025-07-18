
# 🧾 HSRP Redundancy with VLANs & EtherChannel

## 📌 Project Title:
**HSRP VLAN Redundancy with EtherChannel**

---

## 🧠 Project Summary:
This project simulates a redundant network design using **HSRP (Hot Standby Router Protocol)** between two **Multilayer Switches**, ensuring high availability and fault tolerance across multiple VLANs. The design includes **VLAN segmentation**, **inter-VLAN routing**, and **EtherChannel** for link aggregation.

---

## 🖥️ Network Topology:
- 🔁 Two Multilayer Switches running HSRP
- 🔄 EtherChannel connection between switches (Port-channel2)
- 🧱 Two VLANs:  
  - VLAN 10 
  - VLAN 20 
- 🧑‍💻 Multiple End Devices in each VLAN
- 🌐 IP address distribution via **DHCP pools** on the Switch

---

## ⚙️ Key Technologies Used:
- **HSRP** for Gateway Redundancy
- **EtherChannel (Port-channel)** for link aggregation
- **VLANs** and **Inter-VLAN Routing**
- **DHCP Server** configured on the switch
- **Default Gateway Failover Testing**

---

## 🔧 Configuration Highlights:

### HSRP Configuration Example:
```bash
interface Vlan10
  ip address 192.168.10.2 255.255.255.0
  standby 10 ip 192.168.10.1
  standby 10 priority 110
  standby 10 preempt
```

### EtherChannel Example:
```bash
interface range fa0/1 - 2
  channel-group 2 mode active
interface port-channel2
  switchport trunk encapsulation dot1q
  switchport mode trunk
```

### DHCP Pool Example:
```bash
ip dhcp pool manar
  network 192.168.10.0 255.255.255.0
  default-router 192.168.10.1
  dns-server 8.8.8.8
```

---

## ✅ Verification Steps:

- Use `show standby` to verify HSRP roles (Active/Standby)
- Use `show ip dhcp binding` to confirm IP allocation
- Ping Virtual Gateway (e.g., 192.168.10.1) from PCs
- Disconnect Active switch ports → observe **HSRP failover**

---

## 📌 Notes:
- The project **does not include** optional components like Syslog, NTP, or ACLs — to keep focus on the **redundant switching and VLAN structure**.
- The DHCP server is **local**, configured directly on the Multilayer Switch.

---

## 🎯 Purpose:
Demonstrate knowledge in:
- Designing fault-tolerant Layer 3 switching environments
- VLAN segmentation and trunking
- Redundancy protocols (HSRP)
- EtherChannel configuration
