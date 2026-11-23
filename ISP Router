! ISP-Router (Cisco ISR 4331, Packet Tracer)
! Static WAN interface and DHCP server for the Edge-Router
!
enable
configure terminal
!
! WAN interface facing the Edge-Router
interface gigabitEthernet 0/0/0
 ip address 200.1.1.1 255.255.255.0
 no shutdown
 exit
!
! Do not lease the router's own address
ip dhcp excluded-address 200.1.1.1
!
! DHCP pool for the WAN segment
ip dhcp pool ISP-POOL
 network 200.1.1.0 255.255.255.0
 default-router 200.1.1.1
 dns-server 8.8.8.8
 exit
!
end
write memory
