# Device Configurations – CML BGP Project

This file aggregates the configurations of all routers in the CML BGP topology.

---

## R1

```text
Building configuration...

Current configuration : 3793 bytes
!
! Last configuration change at 15:29:44 UTC Tue Dec 9 2025
!
version 15.9
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
no aaa new-model
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface Loopback0
 ip address 119.114.31.1 255.255.255.0
 ipv6 address 2F02:C3D4:E0E0:1000::1/64
!
interface GigabitEthernet0/0
 ip address 11.47.0.1 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E00::1/64
!
interface GigabitEthernet0/1
 ip address 11.47.0.9 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E02::1/64
!
interface GigabitEthernet0/2
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router bgp 65100
 bgp log-neighbor-changes
 neighbor 11.47.0.2 remote-as 65100
 neighbor 11.47.0.2 password bgppass
 neighbor 11.47.0.2 update-source GigabitEthernet0/0
 neighbor 11.47.0.10 remote-as 65100
 neighbor 11.47.0.10 password bgppass
 neighbor 11.47.0.10 update-source GigabitEthernet0/1
 !
 address-family ipv4
  network 119.114.31.0 mask 255.255.255.0
  neighbor 11.47.0.2 activate
  neighbor 11.47.0.10 activate
 exit-address-family
 !
 address-family ipv6
  network 2F02:C3D4:E0E0:1000::/64
  neighbor 11.47.0.2 activate
  neighbor 11.47.0.10 activate
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
ipv6 ioam timestamp
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!
line con 0
 exec-timeout 0 0
line aux 0
line vty 0 4
 exec-timeout 0 0
 login
 transport input none
!
no scheduler allocate
!
end
```

---

## R2

```text
Building configuration...

Current configuration : 3871 bytes
!
! Last configuration change at 15:29:20 UTC Tue Dec 9 2025
!
version 15.9
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R2
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
no aaa new-model
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface GigabitEthernet0/0
 ip address 11.47.0.2 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E00::2/64
!
interface GigabitEthernet0/1
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/2
 ip address 11.47.0.5 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E01::1/64
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router bgp 65100
 bgp log-neighbor-changes
 neighbor 11.47.0.1 remote-as 65100
 neighbor 11.47.0.1 password bgppass
 neighbor 11.47.0.1 update-source GigabitEthernet0/0
 neighbor 11.47.0.6 remote-as 65100
 neighbor 11.47.0.6 password bgppass
 neighbor 11.47.0.6 update-source GigabitEthernet0/2
 !
 address-family ipv4
  neighbor 11.47.0.1 activate
  neighbor 11.47.0.1 route-map FILTER-IN in
  neighbor 11.47.0.6 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 11.47.0.1 activate
  neighbor 11.47.0.6 activate
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
!
ip prefix-list BLOCK-R1-LO seq 5 deny 119.114.31.0/24
ip prefix-list BLOCK-R1-LO seq 10 permit 0.0.0.0/0 le 32
ipv6 ioam timestamp
!
route-map FILTER-IN deny 10
 match ip address prefix-list BLOCK-R1-LO
!
route-map FILTER-IN permit 20
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!
line con 0
 exec-timeout 0 0
line aux 0
line vty 0 4
 exec-timeout 0 0
 login
 transport input none
!
no scheduler allocate
!
end
```

---

## R3

```text
Building configuration...

Current configuration : 3696 bytes
!
! Last configuration change at 15:29:20 UTC Tue Dec 9 2025
!
version 15.9
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R3
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
no aaa new-model
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface GigabitEthernet0/0
 ip address 11.47.0.13 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E03::1/64
!
interface GigabitEthernet0/1
 ip address 11.47.0.10 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E02::2/64
!
interface GigabitEthernet0/2
 ip address 11.47.0.6 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E01::2/64
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router bgp 65100
 bgp log-neighbor-changes
 neighbor 11.47.0.5 remote-as 65100
 neighbor 11.47.0.5 password bgppass
 neighbor 11.47.0.9 remote-as 65100
 neighbor 11.47.0.9 password bgppass
 neighbor 11.47.0.14 remote-as 65101
 neighbor 11.47.0.14 password bgppass
 !
 address-family ipv4
  neighbor 11.47.0.5 activate
  neighbor 11.47.0.9 activate
  neighbor 11.47.0.14 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 11.47.0.5 activate
  neighbor 11.47.0.9 activate
  neighbor 11.47.0.14 activate
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
ipv6 ioam timestamp
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!
line con 0
 exec-timeout 0 0
line aux 0
line vty 0 4
 exec-timeout 0 0
 login
 transport input none
!
no scheduler allocate
!
end
```

---

## R4

```text
Building configuration...

Current configuration : 3514 bytes
!
! Last configuration change at 15:31:33 UTC Tue Dec 9 2025
!
version 15.9
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R4
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
no aaa new-model
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface GigabitEthernet0/0
 ip address 11.47.0.14 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E03::2/64
!
interface GigabitEthernet0/1
 ip address 11.41.0.17 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E04::1/64
!
interface GigabitEthernet0/2
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router bgp 65101
 bgp log-neighbor-changes
 neighbor 11.41.0.18 remote-as 65102
 neighbor 11.41.0.18 password bgppass
 neighbor 11.47.0.13 remote-as 65100
 neighbor 11.47.0.13 password bgppass
 !
 address-family ipv4
  neighbor 11.41.0.18 activate
  neighbor 11.47.0.13 activate
 exit-address-family
 !
 address-family ipv6
  neighbor 11.41.0.18 activate
  neighbor 11.47.0.13 activate
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
ipv6 ioam timestamp
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!
line con 0
 exec-timeout 0 0
line aux 0
line vty 0 4
 exec-timeout 0 0
 login
 transport input none
!
no scheduler allocate
!
end
```

---

## R5

```text
Building configuration...

Current configuration : 3456 bytes
!
! Last configuration change at 15:30:01 UTC Tue Dec 9 2025
!
version 15.9
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R5
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
no aaa new-model
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface Loopback0
 ip address 22.55.111.1 255.255.255.0
 ipv6 address A001:A7BD:F911:D000::1/64
!
interface GigabitEthernet0/0
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/1
 ip address 11.41.0.18 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 ipv6 address BB25:FCA4:C6FE:1E04::2/64
!
interface GigabitEthernet0/2
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router bgp 65102
 bgp log-neighbor-changes
 neighbor 11.41.0.17 remote-as 65101
 neighbor 11.41.0.17 password bgppass
 !
 address-family ipv4
  network 0.0.0.0
  neighbor 11.41.0.17 activate
 exit-address-family
 !
 address-family ipv6
  network ::/0
  neighbor 11.41.0.17 activate
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
ipv6 ioam timestamp
!
!
!
control-plane
!
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!
line con 0
 exec-timeout 0 0
line aux 0
line vty 0 4
 exec-timeout 0 0
 login
 transport input none
!
no scheduler allocate
!
end
```

