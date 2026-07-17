# Cisco Enterprise Network Lab

> A physical Cisco networking project demonstrating enterprise routing, switching, wireless infrastructure, dynamic routing, and Internet connectivity using real Cisco hardware.

---

## Project Overview

This project simulates a small enterprise environment consisting of a headquarters campus and a remote branch office connected through a core router.

The network demonstrates common enterprise technologies including:

- Layer 2 Switching
- Layer 3 Routing
- Router-on-a-Stick (RoAS)
- Switch Virtual Interfaces (SVI)
- OSPF Dynamic Routing
- VLAN Segmentation
- DHCP Services
- Cisco Wireless LAN Controller (WLC)
- Lightweight Access Points (CAPWAP)
- Option 43 AP Discovery
- NAT/PAT Internet Access
- EtherChannel
- Port Security
- Voice VLANs
- Enterprise Wireless

The entire lab was built using **physical Cisco routers, switches, and wireless equipment**, providing hands-on experience with technologies commonly deployed in enterprise environments.

---

# Objectives

The primary goals of this project are to:

- Build a scalable enterprise network
- Separate traffic using VLANs
- Route traffic between multiple sites
- Centralise network services
- Deploy Cisco lightweight wireless infrastructure
- Provide Internet access through NAT/PAT
- Demonstrate enterprise troubleshooting techniques

---

# Network Architecture

```
                          Internet
                              │
                    BT Home Hub (192.168.1.254)
                              │
                      Fa0/1 - Outside
                              │
                    ┌──────────────────┐
                    │       R2         │
                    │   Core / Edge    │
                    └──────────────────┘
                     │              │
            Serial0/1/0        FastEthernet0/0
                     │              │
               ┌──────────┐    ┌──────────┐
               │    R1    │    │    R3    │
               │ Campus   │    │ Branch   │
               └──────────┘    └──────────┘
                     │              │
                    SW1        Integrated Switch
                     │              │
             WLC + Enterprise AP   Branch AP
```

---

# Device Roles

## R2 — Core / Edge Router

Acts as the central routing point for the enterprise.

### Responsibilities

- Internet Gateway
- NAT/PAT
- DHCP Server
- DNS Forwarding
- OSPF Backbone
- Option 43 for Cisco AP Discovery

---

## R1 — Enterprise Campus Router

Provides routing for the headquarters network.

### Responsibilities

- Router-on-a-Stick
- Campus VLAN Routing
- Wireless LAN Controller Connectivity
- Enterprise User Networks

---

## R3 — Branch Office Router

Provides routing for the remote office.

### Responsibilities

- Branch VLAN Routing
- Wireless Access Point Connectivity
- Printer & Media Networks

---

## SW1

Campus distribution/access switch.

Provides:

- VLAN Trunking
- EtherChannel
- WLC Connectivity
- AP Connectivity
- Enterprise Access Ports

---

## SW2

Enterprise access switch.

Provides:

- User Access
- Voice VLANs
- Port Security
- EtherChannel Uplink

---

## Cisco Wireless LAN Controller

Provides centralized wireless management.

Responsible for:

- Lightweight AP Management
- CAPWAP
- WLAN Configuration
- Guest Wireless
- Internal Wireless
- Dynamic Interfaces

---

# Technologies Used

| Technology | Purpose |
|------------|---------|
| Cisco IOS | Routing & Switching |
| OSPF | Dynamic Routing |
| NAT Overload (PAT) | Internet Access |
| DHCP | Address Assignment |
| Cisco WLC | Wireless Controller |
| CAPWAP | AP Management |
| EtherChannel (LACP) | Link Aggregation |
| PVST+ | Loop Prevention |
| Port Security | Layer 2 Security |
| Voice VLAN | IP Telephony |
| Option 43 | AP Discovery |
| Telnet / SSH | Device Management |

---

# VLAN Design

| VLAN | Description |
|------|-------------|
|10|Users|
|20|Staff|
|30|Management|
|40|Servers|
|50|Voice|
|99|Native|
|110|Branch Users|
|120|Branch Voice|
|130|Branch Media / Printer|
|201|Internal Wireless|
|202|Guest Wireless|
|210|Branch AP Management|
|211|Branch Guest AP|

---

# Wireless Infrastructure

The wireless environment consists of:

- Cisco Wireless LAN Controller
- Lightweight Cisco Aironet Access Points
- CAPWAP
- Dynamic Interfaces
- Guest WLAN
- Internal WLAN

Access Points automatically discover the controller using **DHCP Option 43**.

---

# Routing

Routing is performed using **OSPF Area 0**.

```
Campus
      \
       \
        R1 -------- R2 -------- R3
             OSPF Backbone
```

The Core Router advertises the default route to both sites.

No static Internet routes are required on R1 or R3.

---

# Internet Access

Only **R2** performs Network Address Translation.

```
Internal Network
        │
        ▼
   R1 / R3
        │
        ▼
        R2
        │
   PAT (Overload)
        │
        ▼
   BT Home Hub
        │
     Internet
```

---

# DHCP

All DHCP services are centralised on **R2**.

DHCP provides addressing for:

- Enterprise Users
- Staff
- Management
- Branch Office
- Wireless Clients
- Cisco Access Points

---

# Security Features

Implemented security mechanisms include:

- Port Security
- BPDU Guard
- PortFast
- Voice VLAN Separation
- Management VLAN
- Access Control Lists
- SSH/Telnet/Webmode Management
- NAT/PAT

---

# Hardware

## Routers

- Cisco 1841
- Cisco 1812

## Switches

- Cisco Catalyst 3560

## Wireless

- Cisco Wireless LAN Controller 2100 Series
- Cisco AIR-CAP3502I-E-K9

