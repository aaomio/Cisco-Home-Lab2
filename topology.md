# Network Topology

## Overview

This lab simulates a small enterprise consisting of a Headquarters (HQ) campus and a remote Branch Office.

The network is divided into three routing domains:

- **R2** – Core / Edge Router
- **R1** – Headquarters Campus
- **R3** – Branch Office

R2 provides centralised services including DHCP, Internet access, NAT/PAT and OSPF routing.

---

# Physical Topology

```
                                         Internet
                                             │
                                             │
                                  BT Home Hub Router
                                   192.168.1.254/24
                                             │
                                  Fa0/1 - 192.168.1.2
                                             │
                                   ┌─────────────────┐
                                   │       R2        │
                                   │ Core / Edge     │
                                   └─────────────────┘
                                     │           │
                        Serial0/1/0  │           │ Fa0/0
                         10.0.0.2     │           │10.0.1.2
                                     │           │
                                     │           │
                              10.0.0.1           │10.0.1.1
                                     │           │
                           ┌──────────┘           └──────────┐
                           │                                │
                    ┌────────────┐                 ┌────────────┐
                    │    R1      │                 │    R3      │
                    │ HQ Router  │                 │ Branch     │
                    └────────────┘                 └────────────┘
                           │                                │
                           │802.1Q                          │Integrated Switch
                           │                                │
                    ┌────────────┐                  Cisco 1812 ESW
                    │    SW1     │
                    └────────────┘
                      │        │
                      │        │
               Cisco WLC     SW2
                      │
                Lightweight AP
```

---

# Router Links

| Link | Network |
|-------|----------|
|R1 ⇄ R2|10.0.0.0/30|
|R2 ⇄ R3|10.0.1.0/30|
|R2 ⇄ BT Router|192.168.1.0/24|

---

# Router IP Addressing

## R1

| Interface | Address |
|-----------|----------|
|Fa0/0.10|192.168.10.1/24|
|Fa0/0.20|192.168.20.1/24|
|Fa0/0.30|192.168.30.1/24|
|Fa0/0.40|192.168.40.1/24|
|Fa0/0.50|192.168.50.1/24|
|Fa0/0.201|192.168.201.1/24|
|Fa0/0.202|192.168.202.1/24|
|Serial0/1/0|10.0.0.1/30|

---

## R2 (Core)

| Interface | Address |
|-----------|----------|
|Serial0/1/0|10.0.0.2/30|
|Fa0/0|10.0.1.2/30|
|Fa0/1 (Internet)|192.168.1.2/24|

Default Gateway (ISP)

```
192.168.1.254
```

---

## R3

| Interface | Address |
|-----------|----------|
|Fa1|10.0.1.1/30|
|VLAN110|192.168.110.1/24|
|VLAN120|192.168.120.1/24|
|VLAN130|192.168.130.1/24|
|VLAN211|192.168.211.1/24|
|VLAN212|192.168.212.1/24|

---

# VLAN Design

## Headquarters

| VLAN | Name | Gateway |
|------|------|----------|
|10|Users|192.168.10.1|
|20|Staff|192.168.20.1|
|30|Management|192.168.30.1|
|40|Servers|192.168.40.1|
|50|Voice|192.168.50.1|
|99|Native|None|
|201|Internal Wireless|192.168.201.1|
|202|Guest Wireless|192.168.202.1|

---

## Branch Office

| VLAN | Name | Gateway |
|------|------|----------|
|110|Users|192.168.110.1|
|120|Voice|192.168.120.1|
|130|Printer / Media|192.168.130.1|
|211|AP Management|192.168.211.1|
|212|Guest AP|192.168.212.1|

---

# Subnet Summary

| Network | Purpose |
|-----------|-------------|
|192.168.1.0/24|Internet / ISP|
|10.0.0.0/30|R1 ↔ R2|
|10.0.1.0/30|R2 ↔ R3|
|192.168.10.0/24|HQ Users|
|192.168.20.0/24|HQ Staff|
|192.168.30.0/24|Management|
|192.168.40.0/24|Servers|
|192.168.50.0/24|Voice|
|192.168.110.0/24|Branch Users|
|192.168.120.0/24|Branch Voice|
|192.168.130.0/24|Printer / Media|
|192.168.201.0/24|Internal Wi-Fi|
|192.168.202.0/24|Guest Wi-Fi|
|192.168.211.0/24|Branch AP|
|192.168.212.0/24|Branch Guest AP|

---

# Wireless Infrastructure

## Cisco WLC

Management Interface

```
192.168.30.20
```

Connected to

```
SW1 Fa0/1
```

---

## Headquarters AP

| Device | VLAN | IP |
|---------|------|------|
|Internal AP|201|192.168.201.254|

Provides

- Internal WLAN
- Guest WLAN

---

## Branch AP

| Device | VLAN | IP |
|---------|------|------|
|Branch AP|212|192.168.212.2 (DHCP)|

Provides

- Branch wireless coverage
- CAPWAP tunnel back to HQ WLC

---

# DHCP

All DHCP services are hosted on **R2**.

Served Networks

- VLAN10
- VLAN20
- VLAN30
- VLAN40
- VLAN50
- VLAN110
- VLAN120
- VLAN130
- VLAN201
- VLAN202
- VLAN211
- VLAN212

Cisco AP discovery is performed using **DHCP Option 43**.

---

# Dynamic Routing

Routing Protocol

```
OSPF Process 1
Area 0
```

Router IDs

| Router | Router ID |
|---------|-----------|
|R1|1.1.1.1|
|R2|2.2.2.2|
|R3|3.3.3.3|

---

# Internet Access

R2 is the enterprise edge router.

Responsibilities

- Default Route
- NAT Overload (PAT)
- Internet Gateway

Traffic Flow

```
Client
   │
R1 / R3
   │
   ▼
R2
   │
PAT
   │
BT Router
   │
Internet
```

---

# Management Addresses

| Device | Address |
|---------|----------|
|R1|10.0.0.1|
|R2|10.0.0.2 / 10.0.1.2|
|R3|10.0.1.1|
|SW1|192.168.30.11|
|SW2|192.168.30.12|
|WLC|192.168.30.20|

---

# Design Summary

- R2 acts as the Enterprise Core and Internet Edge.
- R1 provides Router-on-a-Stick routing for the HQ campus.
- R3 provides Layer 3 routing for the branch office using SVIs.
- DHCP is centralised on R2.
- Wireless is centralised using a Cisco Wireless LAN Controller.
- Both Access Points discover the controller using DHCP Option 43 and CAPWAP.
- OSPF dynamically advertises all internal routes while R2 provides Internet connectivity using NAT/PAT.