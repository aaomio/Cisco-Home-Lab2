Building configuration...

Current configuration : 4208 bytes
!
version 12.2
no service pad
service timestamps debug uptime
service timestamps log uptime
no service password-encryption
!
hostname SW2
!
enable secret 5 $
enable password $
!
username admin privilege 15 secret 5 $
no aaa new-model
system mtu routing 1500
ip subnet-zero
ip domain-name local.lab
!
!
!
!
errdisable recovery cause psecure-violation
errdisable recovery interval 30
no file verify auto
spanning-tree mode pvst
spanning-tree portfast default
spanning-tree portfast bpduguard default
spanning-tree extend system-id
!
vlan internal allocation policy ascending
!
!
interface Port-channel1
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
 switchport port-security mac-address sticky
 switchport port-security mac-address sticky 24fb.e3c0.313c
!
interface FastEthernet0/2
 switchport access vlan 40
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/3
 switchport access vlan 10
 switchport mode access
 switchport port-security mac-address sticky
!
interface FastEthernet0/4
 switchport access vlan 40
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/5
 switchport access vlan 10
 switchport mode access
 switchport port-security mac-address sticky
!
interface FastEthernet0/6
 switchport access vlan 40
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/7
 switchport access vlan 10
 switchport mode access
 switchport port-security mac-address sticky
!
interface FastEthernet0/8
 switchport access vlan 40
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/9
 switchport access vlan 10
 switchport mode access
 switchport port-security mac-address sticky
!
interface FastEthernet0/10
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/11
!
interface FastEthernet0/12
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/13
 switchport access vlan 20
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky
 switchport port-security mac-address sticky c03e.ba87.085b
!
interface FastEthernet0/14
 switchport access vlan 50
 switchport mode access
 switchport voice vlan 50
 spanning-tree portfast
!
interface FastEthernet0/15
 switchport access vlan 20
 switchport mode access
 switchport port-security maximum 2
 switchport port-security
 switchport port-security mac-address sticky
 spanning-tree portfast
!
interface FastEthernet0/16
 switchport access vlan 50
 switchport mode access
 switchport voice vlan 50
 spanning-tree portfast
!
interface FastEthernet0/17
 switchport access vlan 20
 switchport mode access
 switchport port-security
!
interface FastEthernet0/18
 switchport access vlan 50
 switchport mode access
 switchport voice vlan 50
 spanning-tree portfast
!
interface FastEthernet0/19
 switchport access vlan 20
 switchport mode access
 switchport port-security maximum 2
 switchport port-security
 switchport port-security mac-address sticky
 switchport port-security mac-address sticky 24fb.e3c0.313c
!
interface FastEthernet0/20
!
interface FastEthernet0/21
 switchport access vlan 20
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
!
interface Vlan30
 ip address 192.168.30.12 255.255.255.0
!
ip default-gateway 192.168.30.1
ip classless
ip http server
!
!
!
control-plane
!
!
line con 0
 logging synchronous
line vty 0 4
 exec-timeout 5 0
 password Darko
 login local
 transport input telnet
line vty 5 15
 exec-timeout 5 0
 password Darko
 login local
 transport input telnet
!
end
