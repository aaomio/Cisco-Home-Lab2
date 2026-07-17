Building configuration...

Current configuration : 2713 bytes
!
version 12.2
no service pad
service timestamps debug uptime
service timestamps log uptime
no service password-encryption
!
hostname SW1
!
enable secret 5 $
!
username Admin privilege 15 secret 5 $
no aaa new-model
system mtu routing 1500
ip subnet-zero
ip domain-name lab.local
ip host SW2 192.168.30.12
!
!
!
!
no file verify auto
!
spanning-tree mode pvst
spanning-tree extend system-id
spanning-tree vlan 10,20,30,99,201 priority 24576
!
vlan internal allocation policy ascending
!
!
interface Port-channel1
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99,201,202
 switchport mode trunk
!
interface FastEthernet0/1
 description Cisco WLC
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 30
 switchport trunk allowed vlan 30,201
 switchport mode trunk
!
interface FastEthernet0/2
!
interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access
 switchport port-security
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99,201,202
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/11
 description *** R1 Router-on-a-Stick ***
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99,201,202
 switchport mode trunk
!
interface FastEthernet0/12
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99,201,202
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/13
 power inline consumption 15000
 switchport access vlan 201
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/14
!
interface FastEthernet0/15
 power inline consumption 15000
 switchport access vlan 202
 switchport mode access
 spanning-tree portfast
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
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
 ip address 192.168.30.11 255.255.255.0
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
line vty 0 4
 login local
 transport input telnet
line vty 5 15
 login local
 transport input telnet
!
end

