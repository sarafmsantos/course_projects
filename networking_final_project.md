Project of a Corporate Network Infrastructure in Cisco Packet Tracer

Network Topology:
- 2 locations: Corporate + Branch
- 6 Local Area Networks (LAN) + 4 Virtual LANs (VLAN)
<img width="1084" height="560" alt="image" src="https://github.com/user-attachments/assets/3dd0bcf6-fa8c-47dd-a980-43f35b4cdb86" />


OSPF with authentication:
<img width="1083" height="559" alt="image" src="https://github.com/user-attachments/assets/ca739b44-5ac9-4b7a-a434-acb89ea8447e" />


DHCP:
<img width="1083" height="558" alt="image" src="https://github.com/user-attachments/assets/ac86af91-542e-4ae4-9a91-6672b72948da" />


NAT / PAT:
<img width="1083" height="558" alt="image" src="https://github.com/user-attachments/assets/644c6fdd-5e69-4351-91bb-e49ced4a216e" />


Site-to-site VPN:
<img width="1081" height="559" alt="image" src="https://github.com/user-attachments/assets/1bba96b8-f24a-4715-b782-93f8b6f2e0f4" />


Services and protocols:
- AD with LDAP
- Kerberos authentication
- SMTP
- SYSLOG
- HTTPS
- SMB 
- proprietary application for internal communication running on port range 31000–31002 on servers MODEL-1 and MODEL-2
- intranet named "intra-QWERTYcorp.org" hosted in DC02

ACLs:
- PC NetAdmin is the only host allowed to remotely access all the other equipments in both Corporate and Branch networks
- All servers outside the DMZ must not be able to communicate with the public network
- Exception to the previous rule: SYSLOG server on TCP port 6514 and NAS-2 server on the RDP port

Full Packet Tracer log:
Wed Jan 21 21:34:04 2026   CORE-EDGE   Router>ena
Wed Jan 21 21:34:06 2026   CORE-EDGE   Router#conf t
Wed Jan 21 21:41:09 2026   CORE-EDGE   Router(config)#hostname CORE-EDGE
Wed Jan 21 21:41:17 2026   CORE-EDGE   CORE-EDGE(config)#line con 0
Wed Jan 21 21:41:53 2026   CORE-EDGE   CORE-EDGE(config-line)#password CISEGCISCO
Wed Jan 21 21:41:55 2026   CORE-EDGE   CORE-EDGE(config-line)#login
Wed Jan 21 21:41:58 2026   CORE-EDGE   CORE-EDGE(config-line)#exit
Wed Jan 21 21:42:14 2026   CORE-EDGE   CORE-EDGE(config)#enable secret CISEGCISCO
Wed Jan 21 21:42:20 2026   CORE-EDGE   CORE-EDGE(config)#line vty 0 15
Wed Jan 21 21:42:29 2026   CORE-EDGE   CORE-EDGE(config-line)#password CISEGCISCO
Wed Jan 21 21:42:35 2026   CORE-EDGE   CORE-EDGE(config-line)#login
Wed Jan 21 21:42:36 2026   CORE-EDGE   CORE-EDGE(config-line)#exit
Wed Jan 21 21:47:34 2026   CORE-EDGE   CORE-EDGE(config)#login
Wed Jan 21 21:47:46 2026   CORE-EDGE   CORE-EDGE(config)#line vty 0 15
Wed Jan 21 21:47:52 2026   CORE-EDGE   CORE-EDGE(config-line)#password CISEGCISCO
Wed Jan 21 21:47:56 2026   CORE-EDGE   CORE-EDGE(config-line)#login
Wed Jan 21 21:48:00 2026   CORE-EDGE   CORE-EDGE(config-line)#exit
Wed Jan 21 21:49:43 2026   CORE-EDGE   CORE-EDGE(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 21:52:02 2026   CORE-EDGE   CORE-EDGE(config)#service password-encryption
Wed Jan 21 21:52:24 2026   CORE-EDGE   CORE-EDGE(config)#security passwords min-length 10
Wed Jan 21 21:53:09 2026   CORE-EDGE   CORE-EDGE(config)#login block-for 90 attempts 2 within 10
Wed Jan 21 21:53:25 2026   CORE-EDGE   CORE-EDGE(config)#service timestamps log datetime msec
Wed Jan 21 21:55:10 2026   CORE-EDGE   CORE-EDGE(config)#ip domain-name QWERTYCorp.org
Wed Jan 21 21:55:21 2026   CORE-EDGE   CORE-EDGE(config)#username admin secret CISEGCISCO
Wed Jan 21 21:55:35 2026   CORE-EDGE   CORE-EDGE(config)#crypto key generate rsa general-keys modulus 1024
Wed Jan 21 21:55:47 2026   CORE-EDGE   CORE-EDGE(config)#ip ssh version 2
Wed Jan 21 21:55:59 2026   CORE-EDGE   CORE-EDGE(config)#ip ssh tim-out 90
Wed Jan 21 21:56:05 2026   CORE-EDGE   CORE-EDGE(config)#ip ssh time-out 90
Wed Jan 21 21:56:17 2026   CORE-EDGE   CORE-EDGE(config)#ip ssh authentication-retries 2
Wed Jan 21 21:56:23 2026   CORE-EDGE   CORE-EDGE(config)#line vty 0 15
Wed Jan 21 21:56:27 2026   CORE-EDGE   CORE-EDGE(config-line)#login local
Wed Jan 21 21:56:33 2026   CORE-EDGE   CORE-EDGE(config-line)#transport input ssh
Wed Jan 21 21:56:50 2026   CORE-EDGE   CORE-EDGE(config-line)#exit
Wed Jan 21 21:57:01 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/0
Wed Jan 21 21:57:19 2026   CORE-EDGE   CORE-EDGE(config-if)#ip address 203.0.113.1 255.255.255.0
Wed Jan 21 21:57:48 2026   CORE-EDGE   CORE-EDGE(config-if)#no shut
Wed Jan 21 21:57:52 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Wed Jan 21 21:58:21 2026   CORE-EDGE   CORE-EDGE(config)#description Ligacao ao router ISP
Wed Jan 21 21:59:02 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/0
Wed Jan 21 21:59:12 2026   CORE-EDGE   CORE-EDGE(config-if)#description Ligacao ao router ISP
Wed Jan 21 21:59:54 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Wed Jan 21 22:00:01 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/1
Wed Jan 21 22:00:26 2026   CORE-EDGE   CORE-EDGE(config-if)#description Ligacao ao CORE-MLS-1
Wed Jan 21 22:03:12 2026   CORE-EDGE   CORE-EDGE(config-if)#ip address 172.16.2.1 255.255.255.248
Wed Jan 21 22:03:21 2026   CORE-EDGE   CORE-EDGE(config-if)#no shut
Wed Jan 21 22:03:28 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Wed Jan 21 22:03:35 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/2
Wed Jan 21 22:04:02 2026   CORE-EDGE   CORE-EDGE(config-if)#description Ligacao ao switch DMZ-SW
Wed Jan 21 22:05:14 2026   CORE-EDGE   CORE-EDGE(config-if)#ip address 172.16.1.1 255.255.255.128
Wed Jan 21 22:05:21 2026   CORE-EDGE   CORE-EDGE(config-if)#no shut
Wed Jan 21 22:06:21 2026   CORE-EDGE   CORE-EDGE(config-if)#end
Wed Jan 21 22:06:29 2026   CORE-EDGE   CORE-EDGE#copy run start
Wed Jan 21 22:06:53 2026   ISP   Router>ena
Wed Jan 21 22:06:55 2026   ISP   Router#conf t
Wed Jan 21 22:07:04 2026   ISP   Router(config)#hostname ISP
Wed Jan 21 22:07:44 2026   ISP   ISP(config)#line con 0
Wed Jan 21 22:07:53 2026   ISP   ISP(config-line)#password CISEGCISCO
Wed Jan 21 22:07:58 2026   ISP   ISP(config-line)#login
Wed Jan 21 22:08:01 2026   ISP   ISP(config-line)#exit
Wed Jan 21 22:08:15 2026   ISP   ISP(config)#enable secret CISEGCISCO
Wed Jan 21 22:08:20 2026   ISP   ISP(config)#line vty 0 15
Wed Jan 21 22:08:30 2026   ISP   ISP(config-line)#password CISEGCISCO
Wed Jan 21 22:08:35 2026   ISP   ISP(config-line)#login
Wed Jan 21 22:08:37 2026   ISP   ISP(config-line)#exit
Wed Jan 21 22:09:40 2026   ISP   ISP(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 22:10:01 2026   ISP   ISP(config)#service password-encryption
Wed Jan 21 22:10:16 2026   ISP   ISP(config)#security passwords min-length 10
Wed Jan 21 22:10:30 2026   ISP   ISP(config)#login block-for 90 attempts 2 within 10
Wed Jan 21 22:10:44 2026   ISP   ISP(config)#service timestamps log datetime msec
Wed Jan 21 22:16:27 2026   ISP   ISP(config)#banner motd "This equipment belongs to the Internet provider. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 22:17:00 2026   ISP   ISP(config)#ip domain-name atec.pt
Wed Jan 21 22:17:28 2026   ISP   ISP(config)#username admin secret CISEGCISCO
Wed Jan 21 22:17:41 2026   ISP   ISP(config)#crypto key generate rsa general-keys modulus 1024
Wed Jan 21 22:17:54 2026   ISP   ISP(config)#ip ssh version 2
Wed Jan 21 22:18:13 2026   ISP   ISP(config)#ip ssh time-out 90
Wed Jan 21 22:18:30 2026   ISP   ISP(config)#ip ssh authentication-retries 2
Wed Jan 21 22:18:41 2026   ISP   ISP(config)#line vty 0 15
Wed Jan 21 22:18:51 2026   ISP   ISP(config-line)#login local
Wed Jan 21 22:19:02 2026   ISP   ISP(config-line)#transport input ssh
Wed Jan 21 22:26:33 2026   ISP   ISP(config-line)#int g0/0/0
Wed Jan 21 22:26:50 2026   ISP   ISP(config-if)#description Ligacao ao router CORE-EDGE
Wed Jan 21 22:27:08 2026   ISP   ISP(config-if)#ip address 203.0.113.254 255.255.255.0
Wed Jan 21 22:27:18 2026   ISP   ISP(config-if)#no shut
Wed Jan 21 22:27:43 2026   ISP   ISP(config-if)#exit
Wed Jan 21 22:27:51 2026   ISP   ISP(config)#int g0/0/2
Wed Jan 21 22:28:10 2026   ISP   ISP(config-if)#description Ligacao ao router BRANCH-1
Wed Jan 21 22:28:29 2026   ISP   ISP(config-if)#ip address 198.51.100.254 255.255.255.0
Wed Jan 21 22:28:31 2026   ISP   ISP(config-if)#no shut
Wed Jan 21 22:28:54 2026   ISP   ISP(config-if)#no shut
Wed Jan 21 22:29:14 2026   ISP   ISP(config-if)#end
Wed Jan 21 22:29:26 2026   ISP   ISP#copy run start
Wed Jan 21 22:29:31 2026   ISP   ISP#configure terminal
Wed Jan 21 22:29:31 2026   ISP   ISP(config)#interface GigabitEthernet0/0/2
Wed Jan 21 22:30:05 2026   BRANCH-1   Router>ena
Wed Jan 21 22:30:06 2026   BRANCH-1   Router#conf t
Wed Jan 21 22:30:15 2026   BRANCH-1   Router(config)#hostname BRANCH-1
Wed Jan 21 22:30:35 2026   BRANCH-1   BRANCH-1(config)#line con 0
Wed Jan 21 22:31:02 2026   BRANCH-1   BRANCH-1(config-line)#password CISEGCISCO
Wed Jan 21 22:31:11 2026   BRANCH-1   BRANCH-1(config-line)#login
Wed Jan 21 22:31:19 2026   BRANCH-1   BRANCH-1(config-line)#exit
Wed Jan 21 22:31:30 2026   BRANCH-1   BRANCH-1(config)#enable secret CISEGCISCO
Wed Jan 21 22:31:40 2026   BRANCH-1   BRANCH-1(config)#line vty 0 15
Wed Jan 21 22:31:51 2026   BRANCH-1   BRANCH-1(config-line)#password CISEGCISCO
Wed Jan 21 22:31:57 2026   BRANCH-1   BRANCH-1(config-line)#login
Wed Jan 21 22:32:00 2026   BRANCH-1   BRANCH-1(config-line)#exit
Wed Jan 21 22:32:30 2026   BRANCH-1   BRANCH-1(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 22:32:42 2026   BRANCH-1   BRANCH-1(config)#service password-encryption
Wed Jan 21 22:32:52 2026   BRANCH-1   BRANCH-1(config)#security passwords min-length 10
Wed Jan 21 22:33:05 2026   BRANCH-1   BRANCH-1(config)#login block-for 90 attempts 2 within 10
Wed Jan 21 22:33:15 2026   BRANCH-1   BRANCH-1(config)#service timestamps log datetime msec
Wed Jan 21 22:33:31 2026   BRANCH-1   BRANCH-1(config)#ip domain-name QWERTYCorp.org
Wed Jan 21 22:33:43 2026   BRANCH-1   BRANCH-1(config)#username admin secret CISEGCISCO
Wed Jan 21 22:33:53 2026   BRANCH-1   BRANCH-1(config)#crypto key generate rsa general-keys modulus 1024
Wed Jan 21 22:34:05 2026   BRANCH-1   BRANCH-1(config)#ip ssh version 2
Wed Jan 21 22:34:14 2026   BRANCH-1   BRANCH-1(config)#ip ssh time-out 90
Wed Jan 21 22:34:25 2026   BRANCH-1   BRANCH-1(config)#ip ssh authentication-retries 2
Wed Jan 21 22:34:35 2026   BRANCH-1   BRANCH-1(config)#line vty 0 15
Wed Jan 21 22:34:43 2026   BRANCH-1   BRANCH-1(config-line)#login local
Wed Jan 21 22:34:57 2026   BRANCH-1   BRANCH-1(config-line)#transport input ssh
Wed Jan 21 22:35:03 2026   BRANCH-1   BRANCH-1(config-line)#exit
Wed Jan 21 22:35:25 2026   BRANCH-1   BRANCH-1(config)#int g0/0/0
Wed Jan 21 22:36:34 2026   BRANCH-1   BRANCH-1(config-if)#description Ligacao ao switch SW-BRANCH-1
Wed Jan 21 22:37:54 2026   BRANCH-1   BRANCH-1(config-if)#ip address 172.24.0.1 255.255.255.0
Wed Jan 21 22:37:59 2026   BRANCH-1   BRANCH-1(config-if)#no shut
Wed Jan 21 22:38:09 2026   BRANCH-1   BRANCH-1(config-if)#int g0/0/2
Wed Jan 21 22:38:20 2026   BRANCH-1   BRANCH-1(config-if)#description Ligacao ao router ISP
Wed Jan 21 22:38:48 2026   BRANCH-1   BRANCH-1(config-if)#ip address 198.51.100.1 255.255.255.0
Wed Jan 21 22:38:55 2026   BRANCH-1   BRANCH-1(config-if)#no shut
Wed Jan 21 22:39:13 2026   BRANCH-1   BRANCH-1(config-if)#exit
Wed Jan 21 22:39:35 2026   BRANCH-1   BRANCH-1(config)#ip route 0.0.0.0 0.0.0.0 198.51.100.254
Wed Jan 21 22:39:40 2026   BRANCH-1   BRANCH-1(config)#end
Wed Jan 21 22:39:44 2026   BRANCH-1   BRANCH-1#copy run start
Wed Jan 21 22:40:00 2026   CORE-EDGE   CORE-EDGE>ENA
Wed Jan 21 22:40:09 2026   CORE-EDGE   CORE-EDGE#conf t
Wed Jan 21 22:40:28 2026   CORE-EDGE   CORE-EDGE(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.254
Wed Jan 21 22:40:30 2026   CORE-EDGE   CORE-EDGE(config)#end
Wed Jan 21 22:40:35 2026   CORE-EDGE   CORE-EDGE#copy run start
Wed Jan 21 22:41:10 2026   OPS-RTR-1   Router>ena
Wed Jan 21 22:41:12 2026   OPS-RTR-1   Router#conf t
Wed Jan 21 22:41:35 2026   OPS-RTR-1   Router(config)#hostname OPS-RTR-1
Wed Jan 21 22:41:43 2026   OPS-RTR-1   OPS-RTR-1(config)#line con 0
Wed Jan 21 22:41:50 2026   OPS-RTR-1   OPS-RTR-1(config-line)#password CISEGCISCO
Wed Jan 21 22:41:54 2026   OPS-RTR-1   OPS-RTR-1(config-line)#login
Wed Jan 21 22:41:56 2026   OPS-RTR-1   OPS-RTR-1(config-line)#exit
Wed Jan 21 22:42:03 2026   OPS-RTR-1   OPS-RTR-1(config)#enable secret CISEGCISCO
Wed Jan 21 22:42:09 2026   OPS-RTR-1   OPS-RTR-1(config)#line vty 0 15
Wed Jan 21 22:42:16 2026   OPS-RTR-1   OPS-RTR-1(config-line)#password CISEGCISCO
Wed Jan 21 22:42:18 2026   OPS-RTR-1   OPS-RTR-1(config-line)#login
Wed Jan 21 22:42:19 2026   OPS-RTR-1   OPS-RTR-1(config-line)#exit
Wed Jan 21 22:42:46 2026   OPS-RTR-1   OPS-RTR-1(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 22:43:03 2026   OPS-RTR-1   OPS-RTR-1(config)#service password-encryption
Wed Jan 21 22:43:19 2026   OPS-RTR-1   OPS-RTR-1(config)#security passwords min-length 10
Wed Jan 21 22:43:35 2026   OPS-RTR-1   OPS-RTR-1(config)#login block-for 90 attempts 2 within 10
Wed Jan 21 22:43:49 2026   OPS-RTR-1   OPS-RTR-1(config)#service timestamps log datetime msec
Wed Jan 21 22:44:08 2026   OPS-RTR-1   OPS-RTR-1(config)#ip domain-name QWERTYCorp.org
Wed Jan 21 22:44:19 2026   OPS-RTR-1   OPS-RTR-1(config)#username admin secret CISEGCISCO
Wed Jan 21 22:44:33 2026   OPS-RTR-1   OPS-RTR-1(config)#crypto key generate rsa general-keys modulus 1024
Wed Jan 21 22:44:43 2026   OPS-RTR-1   OPS-RTR-1(config)#ip ssh version 2
Wed Jan 21 22:44:53 2026   OPS-RTR-1   OPS-RTR-1(config)#ip ssh time-out 90
Wed Jan 21 22:45:04 2026   OPS-RTR-1   OPS-RTR-1(config)#ip ssh authentication-retries 2
Wed Jan 21 22:45:12 2026   OPS-RTR-1   OPS-RTR-1(config)#line vty 0 15
Wed Jan 21 22:45:20 2026   OPS-RTR-1   OPS-RTR-1(config-line)#login local
Wed Jan 21 22:45:29 2026   OPS-RTR-1   OPS-RTR-1(config-line)#transport input ssh
Wed Jan 21 22:45:35 2026   OPS-RTR-1   OPS-RTR-1(config-line)#exiy
Wed Jan 21 22:45:38 2026   OPS-RTR-1   OPS-RTR-1(config-line)#exit
Wed Jan 21 22:45:46 2026   OPS-RTR-1   OPS-RTR-1(config)#int g0/0/0
Wed Jan 21 22:46:04 2026   OPS-RTR-1   OPS-RTR-1(config-if)#description Ligacao ao CORE-MLS-1
Wed Jan 21 22:46:39 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip address 172.16.2.2 255.255.255.248
Wed Jan 21 22:46:42 2026   OPS-RTR-1   OPS-RTR-1(config-if)#no shut
Wed Jan 21 22:47:13 2026   OPS-RTR-1   OPS-RTR-1(config-if)#exit
Wed Jan 21 22:47:17 2026   OPS-RTR-1   OPS-RTR-1(config)#int g0/0/1
Wed Jan 21 22:47:31 2026   OPS-RTR-1   OPS-RTR-1(config-if)#description Ligacao ao switch SOC-SW
Wed Jan 21 22:47:54 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip address 172.16.0.1 255.255.255.0
Wed Jan 21 22:47:57 2026   OPS-RTR-1   OPS-RTR-1(config-if)#no shut
Wed Jan 21 22:48:05 2026   OPS-RTR-1   OPS-RTR-1(config-if)#exit
Wed Jan 21 22:48:14 2026   OPS-RTR-1   OPS-RTR-1(config)#int s0/1/0
Wed Jan 21 22:48:42 2026   OPS-RTR-1   OPS-RTR-1(config-if)#description Ligacao ao router OPS-RTR-2
Wed Jan 21 22:56:36 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip address 172.16.1.225 255.255.255.252
Wed Jan 21 22:56:50 2026   OPS-RTR-1   OPS-RTR-1(config-if)#no shut
Wed Jan 21 22:57:02 2026   OPS-RTR-1   OPS-RTR-1(config-if)#end
Wed Jan 21 22:57:07 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Wed Jan 21 22:58:00 2026   OPS-RTR-2   Router>ena
Wed Jan 21 22:58:02 2026   OPS-RTR-2   Router#conf t
Wed Jan 21 22:58:11 2026   OPS-RTR-2   Router(config)#hostname OPS-RTR-2
Wed Jan 21 22:58:33 2026   OPS-RTR-2   OPS-RTR-2(config)#line con 0
Wed Jan 21 22:58:42 2026   OPS-RTR-2   OPS-RTR-2(config-line)#password CISEGCISCO
Wed Jan 21 22:58:47 2026   OPS-RTR-2   OPS-RTR-2(config-line)#login
Wed Jan 21 22:58:50 2026   OPS-RTR-2   OPS-RTR-2(config-line)#exit
Wed Jan 21 22:58:59 2026   OPS-RTR-2   OPS-RTR-2(config)#enable secret CISEGCISCO
Wed Jan 21 22:59:08 2026   OPS-RTR-2   OPS-RTR-2(config)#line vty 0 15
Wed Jan 21 22:59:16 2026   OPS-RTR-2   OPS-RTR-2(config-line)#password CISEGCISCO
Wed Jan 21 22:59:20 2026   OPS-RTR-2   OPS-RTR-2(config-line)#login
Wed Jan 21 22:59:22 2026   OPS-RTR-2   OPS-RTR-2(config-line)#exit
Wed Jan 21 22:59:42 2026   OPS-RTR-2   OPS-RTR-2(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Wed Jan 21 22:59:54 2026   OPS-RTR-2   OPS-RTR-2(config)#service password-encryption
Wed Jan 21 23:00:03 2026   OPS-RTR-2   OPS-RTR-2(config)#security passwords min-length 10
Wed Jan 21 23:00:14 2026   OPS-RTR-2   OPS-RTR-2(config)#login block-for 90 attempts 2 within 10
Wed Jan 21 23:00:24 2026   OPS-RTR-2   OPS-RTR-2(config)#service timestamps log datetime msec
Wed Jan 21 23:00:33 2026   OPS-RTR-2   OPS-RTR-2(config)#ip domain-name QWERTYCorp.org
Wed Jan 21 23:00:43 2026   OPS-RTR-2   OPS-RTR-2(config)#username admin secret CISEGCISCO
Wed Jan 21 23:00:59 2026   OPS-RTR-2   OPS-RTR-2(config)#crypto key generate rsa general-keys modulus 1024
Wed Jan 21 23:01:10 2026   OPS-RTR-2   OPS-RTR-2(config)#ip ssh version 2
Wed Jan 21 23:01:20 2026   OPS-RTR-2   OPS-RTR-2(config)#ip ssh time-out 90
Wed Jan 21 23:01:31 2026   OPS-RTR-2   OPS-RTR-2(config)#ip ssh authentication-retries 2
Wed Jan 21 23:01:41 2026   OPS-RTR-2   OPS-RTR-2(config)#line vty 0 15
Wed Jan 21 23:01:49 2026   OPS-RTR-2   OPS-RTR-2(config-line)#login local
Wed Jan 21 23:01:58 2026   OPS-RTR-2   OPS-RTR-2(config-line)#transport input ssh
Wed Jan 21 23:02:02 2026   OPS-RTR-2   OPS-RTR-2(config-line)#exiy
Wed Jan 21 23:02:05 2026   OPS-RTR-2   OPS-RTR-2(config-line)#exit
Wed Jan 21 23:02:14 2026   OPS-RTR-2   OPS-RTR-2(config)#int g0/0/0
Wed Jan 21 23:02:38 2026   OPS-RTR-2   OPS-RTR-2(config-if)#description Ligacao ao switch SERV-FARM-SW
Wed Jan 21 23:04:22 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip address 172.16.1.193 255.255.255.224
Wed Jan 21 23:04:27 2026   OPS-RTR-2   OPS-RTR-2(config-if)#no shut
Wed Jan 21 23:04:33 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Wed Jan 21 23:04:40 2026   OPS-RTR-2   OPS-RTR-2(config)#int g0/0/1
Wed Jan 21 23:05:53 2026   OPS-RTR-2   OPS-RTR-2(config-if)#description Ligacao ao switch MGMT-SW
Wed Jan 21 23:06:28 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip address 172.16.1.129 255.255.255.192
Wed Jan 21 23:06:31 2026   OPS-RTR-2   OPS-RTR-2(config-if)#no shut
Wed Jan 21 23:06:49 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Wed Jan 21 23:06:57 2026   OPS-RTR-2   OPS-RTR-2(config)#int s0/1/0
Wed Jan 21 23:07:08 2026   OPS-RTR-2   OPS-RTR-2(config-if)#description Ligacao ao router OPS-RTR-1
Wed Jan 21 23:08:11 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip address 172.16.1.226 255.255.255.252
Wed Jan 21 23:08:17 2026   OPS-RTR-2   OPS-RTR-2(config-if)#no shut
Wed Jan 21 23:09:01 2026   OPS-RTR-2   OPS-RTR-2(config-if)#end
Wed Jan 21 23:09:05 2026   OPS-RTR-2   OPS-RTR-2#copy run start
Thu Jan 22 12:15:36 2026   DMZ-SW   Switch>ena
Thu Jan 22 12:15:39 2026   DMZ-SW   Switch#conf t
Thu Jan 22 12:19:10 2026   DMZ-SW   Switch(config)#hostname DMZ-SW
Thu Jan 22 12:20:02 2026   DMZ-SW   DMZ-SW(config)#line con 0line con 0
Thu Jan 22 12:20:11 2026   DMZ-SW   DMZ-SW(config)#line con 0
Thu Jan 22 12:20:25 2026   DMZ-SW   DMZ-SW(config-line)#password CISEGCISCO
Thu Jan 22 12:20:29 2026   DMZ-SW   DMZ-SW(config-line)#login
Thu Jan 22 12:20:31 2026   DMZ-SW   DMZ-SW(config-line)#exit
Thu Jan 22 12:20:40 2026   DMZ-SW   DMZ-SW(config)#enable secret CISEGCISCO
Thu Jan 22 12:20:50 2026   DMZ-SW   DMZ-SW(config)#line vty 0 15
Thu Jan 22 12:20:59 2026   DMZ-SW   DMZ-SW(config-line)#password CISEGCISCO
Thu Jan 22 12:21:04 2026   DMZ-SW   DMZ-SW(config-line)#login exit
Thu Jan 22 12:21:07 2026   DMZ-SW   DMZ-SW(config-line)#login
Thu Jan 22 12:21:09 2026   DMZ-SW   DMZ-SW(config-line)#exit
Thu Jan 22 12:21:33 2026   DMZ-SW   DMZ-SW(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 12:21:45 2026   DMZ-SW   DMZ-SW(config)#service password-encryption
Thu Jan 22 12:21:54 2026   DMZ-SW   DMZ-SW(config)#service timestamps log datetime msec
Thu Jan 22 12:22:08 2026   DMZ-SW   DMZ-SW(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 12:22:20 2026   DMZ-SW   DMZ-SW(config)#username admin secret CISEGCISCO
Thu Jan 22 12:22:30 2026   DMZ-SW   DMZ-SW(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 12:22:47 2026   DMZ-SW   DMZ-SW(config)#ip ssh version 2
Thu Jan 22 12:22:57 2026   DMZ-SW   DMZ-SW(config)#ip ssh time-out 90
Thu Jan 22 12:23:09 2026   DMZ-SW   DMZ-SW(config)#ip ssh authentication-retries 2
Thu Jan 22 12:23:18 2026   DMZ-SW   DMZ-SW(config)#line vty 0 15
Thu Jan 22 12:24:01 2026   DMZ-SW   DMZ-SW(config-line)#login local
Thu Jan 22 12:24:11 2026   DMZ-SW   DMZ-SW(config-line)#transport input ssh
Thu Jan 22 12:24:23 2026   DMZ-SW   DMZ-SW(config-line)#exiy
Thu Jan 22 12:24:26 2026   DMZ-SW   DMZ-SW(config-line)#exit
Thu Jan 22 12:25:41 2026   DMZ-SW   DMZ-SW(config)#ip default-gateway 172.16.1.1
Thu Jan 22 12:26:10 2026   DMZ-SW   DMZ-SW(config)#int vlan 1
Thu Jan 22 12:26:33 2026   DMZ-SW   DMZ-SW(config-if)#ip address 172.16.1.2 255.255.255.128
Thu Jan 22 12:26:43 2026   DMZ-SW   DMZ-SW(config-if)#no shut
Thu Jan 22 12:29:00 2026   DMZ-SW   DMZ-SW(config-if)#exit
Thu Jan 22 12:29:09 2026   DMZ-SW   DMZ-SW(config)#int g0/1
Thu Jan 22 12:30:05 2026   DMZ-SW   DMZ-SW(config-if)#description Ligacao ao router CORE-EDGE
Thu Jan 22 12:30:14 2026   DMZ-SW   DMZ-SW(config-if)#int f0/1
Thu Jan 22 12:30:41 2026   DMZ-SW   DMZ-SW(config-if)#description Ligacao ao WebServer
Thu Jan 22 12:30:46 2026   DMZ-SW   DMZ-SW(config-if)#int f0/2
Thu Jan 22 12:31:04 2026   DMZ-SW   DMZ-SW(config-if)#description Ligacao ao FileServer
Thu Jan 22 12:31:08 2026   DMZ-SW   DMZ-SW(config-if)#int f0/3
Thu Jan 22 12:31:19 2026   DMZ-SW   DMZ-SW(config-if)#description Ligacao ao DomainServer
Thu Jan 22 12:32:25 2026   DMZ-SW   DMZ-SW(config-if)#int range f0/4-24, g0/2
Thu Jan 22 12:32:34 2026   DMZ-SW   DMZ-SW(config-if-range)#shut
Thu Jan 22 12:33:22 2026   DMZ-SW   DMZ-SW(config-if-range)#end
Thu Jan 22 12:33:27 2026   DMZ-SW   DMZ-SW#copy run start
Thu Jan 22 12:36:17 2026   SW-BRANCH-1   Switch>ena
Thu Jan 22 12:36:19 2026   SW-BRANCH-1   Switch#conf t
Thu Jan 22 12:36:27 2026   SW-BRANCH-1   Switch(config)#hostname SW-BRANCH-1
Thu Jan 22 12:36:50 2026   SW-BRANCH-1   SW-BRANCH-1(config)#line con 0
Thu Jan 22 12:36:58 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#password CISEGCISCO
Thu Jan 22 12:37:02 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#login
Thu Jan 22 12:37:04 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#exit
Thu Jan 22 12:37:15 2026   SW-BRANCH-1   SW-BRANCH-1(config)#enable secret CISEGCISCO
Thu Jan 22 12:37:24 2026   SW-BRANCH-1   SW-BRANCH-1(config)#line vty 0 15
Thu Jan 22 12:37:33 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#password CISEGCISCO
Thu Jan 22 12:37:36 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#login
Thu Jan 22 12:37:38 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#exit
Thu Jan 22 12:38:12 2026   SW-BRANCH-1   SW-BRANCH-1(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 12:38:23 2026   SW-BRANCH-1   SW-BRANCH-1(config)#service password-encryption
Thu Jan 22 12:38:33 2026   SW-BRANCH-1   SW-BRANCH-1(config)#service timestamps log datetime msec
Thu Jan 22 12:38:42 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 12:38:51 2026   SW-BRANCH-1   SW-BRANCH-1(config)#username admin secret CISEGCISCO
Thu Jan 22 12:39:01 2026   SW-BRANCH-1   SW-BRANCH-1(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 12:39:15 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ip ssh version 2
Thu Jan 22 12:39:29 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ip ssh time-out 90
Thu Jan 22 12:39:41 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ip ssh authentication-retries 2
Thu Jan 22 12:39:50 2026   SW-BRANCH-1   SW-BRANCH-1(config)#line vty 0 15
Thu Jan 22 12:39:58 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#login local
Thu Jan 22 12:40:08 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#transport input ssh
Thu Jan 22 12:41:04 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#ip default-gateway 172.24.0.1
Thu Jan 22 12:41:13 2026   SW-BRANCH-1   SW-BRANCH-1(config)#int vlan 1
Thu Jan 22 12:42:21 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#ip address 172.24.0.2 255.255.255.0
Thu Jan 22 12:42:24 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#no shut
Thu Jan 22 12:42:31 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#exit
Thu Jan 22 12:42:52 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ip default-gateway 172.24.0.1
Thu Jan 22 12:43:13 2026   SW-BRANCH-1   SW-BRANCH-1(config)#int g0/1
Thu Jan 22 12:43:39 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#description Ligacao ao router BRANCH-1
Thu Jan 22 12:43:48 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#no shut
Thu Jan 22 12:44:16 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#int f0/1
Thu Jan 22 12:44:33 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#description Ligacao ao servidor NAS-2
Thu Jan 22 12:44:37 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#no shut
Thu Jan 22 12:44:42 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#int f0/2
Thu Jan 22 12:44:54 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#description Ligacao ao PC0
Thu Jan 22 12:44:57 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#no shut
Thu Jan 22 12:45:03 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#int f0/3
Thu Jan 22 12:45:17 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#description Ligacao ao PC1
Thu Jan 22 12:45:20 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#no shut
Thu Jan 22 12:47:17 2026   SW-BRANCH-1   SW-BRANCH-1(config-if)#int range f0/4-24, g0/2
Thu Jan 22 12:47:21 2026   SW-BRANCH-1   SW-BRANCH-1(config-if-range)#shut
Thu Jan 22 12:47:30 2026   SW-BRANCH-1   SW-BRANCH-1(config-if-range)#end
Thu Jan 22 12:47:33 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Thu Jan 22 15:43:00 2026   SOC-SW   Switch>ena
Thu Jan 22 15:43:03 2026   SOC-SW   Switch#conf t
Thu Jan 22 15:44:02 2026   SOC-SW   Switch(config)#hostname SOC-SW
Thu Jan 22 15:45:15 2026   SOC-SW   SOC-SW(config)#line con 0
Thu Jan 22 15:45:26 2026   SOC-SW   SOC-SW(config-line)#password CISEGCISCO
Thu Jan 22 15:45:38 2026   SOC-SW   SOC-SW(config-line)#login
Thu Jan 22 15:45:48 2026   SOC-SW   SOC-SW(config-line)#exit
Thu Jan 22 15:46:00 2026   SOC-SW   SOC-SW(config)#enable secret CISEGCISCO
Thu Jan 22 15:46:11 2026   SOC-SW   SOC-SW(config)#line vty 0 15
Thu Jan 22 15:46:22 2026   SOC-SW   SOC-SW(config-line)#password CISEGCISCO
Thu Jan 22 15:46:33 2026   SOC-SW   SOC-SW(config-line)#login
Thu Jan 22 15:46:42 2026   SOC-SW   SOC-SW(config-line)#exit
Thu Jan 22 15:47:06 2026   SOC-SW   SOC-SW(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 15:47:19 2026   SOC-SW   SOC-SW(config)#service password-encryption
Thu Jan 22 15:47:30 2026   SOC-SW   SOC-SW(config)#service timestamps log datetime msec
Thu Jan 22 15:47:42 2026   SOC-SW   SOC-SW(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 15:47:52 2026   SOC-SW   SOC-SW(config)#username admin secret CISEGCISCO
Thu Jan 22 15:48:03 2026   SOC-SW   SOC-SW(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 15:48:18 2026   SOC-SW   SOC-SW(config)#ip ssh version 2
Thu Jan 22 15:48:28 2026   SOC-SW   SOC-SW(config)#ip ssh time-out 90
Thu Jan 22 15:48:40 2026   SOC-SW   SOC-SW(config)#ip ssh authentication-retries 2
Thu Jan 22 15:48:52 2026   SOC-SW   SOC-SW(config)#line vty 0 15
Thu Jan 22 15:49:02 2026   SOC-SW   SOC-SW(config-line)#login local
Thu Jan 22 15:49:17 2026   SOC-SW   SOC-SW(config-line)#transport input ssh
Thu Jan 22 15:49:28 2026   SOC-SW   SOC-SW(config-line)#exit
Thu Jan 22 15:51:31 2026   SOC-SW   SOC-SW(config)#ip default-gateway 172.16.0.1 255.255.255.0
Thu Jan 22 15:52:01 2026   SOC-SW   SOC-SW(config)#ip default-gateway 172.16.0.1
Thu Jan 22 15:52:18 2026   SOC-SW   SOC-SW(config)#int vlan 1
Thu Jan 22 15:52:40 2026   SOC-SW   SOC-SW(config-if)#ip address 172.16.0.2 255.255.255.0
Thu Jan 22 15:52:45 2026   SOC-SW   SOC-SW(config-if)#no shut
Thu Jan 22 15:53:12 2026   SOC-SW   SOC-SW(config-if)#int g0/1
Thu Jan 22 15:53:53 2026   SOC-SW   SOC-SW(config-if)#description Ligacao ao router OPS-RTR-1
Thu Jan 22 15:53:59 2026   SOC-SW   SOC-SW(config-if)#no shut
Thu Jan 22 15:54:19 2026   SOC-SW   SOC-SW(config-if)#int f0/1
Thu Jan 22 15:54:39 2026   SOC-SW   SOC-SW(config-if)#description Ligacao ao PC2
Thu Jan 22 15:54:44 2026   SOC-SW   SOC-SW(config-if)#no shut
Thu Jan 22 15:54:53 2026   SOC-SW   SOC-SW(config-if)#int f0/2
Thu Jan 22 15:55:11 2026   SOC-SW   SOC-SW(config-if)#description Ligacao ao PC3
Thu Jan 22 15:55:15 2026   SOC-SW   SOC-SW(config-if)#no shut
Thu Jan 22 15:55:20 2026   SOC-SW   SOC-SW(config-if)#int f0/3
Thu Jan 22 15:55:47 2026   SOC-SW   SOC-SW(config-if)#description Ligacao ao servidor SYSLOG
Thu Jan 22 15:55:50 2026   SOC-SW   SOC-SW(config-if)#no shut
Thu Jan 22 15:56:30 2026   SOC-SW   SOC-SW(config-if)#int range f0/4-24, g0/2
Thu Jan 22 15:56:33 2026   SOC-SW   SOC-SW(config-if-range)#shut
Thu Jan 22 15:56:44 2026   SOC-SW   SOC-SW(config-if-range)#end
Thu Jan 22 15:56:58 2026   SOC-SW   SOC-SW#copy run start
Thu Jan 22 16:00:33 2026   MGMT-SW   Switch>ena
Thu Jan 22 16:00:37 2026   MGMT-SW   Switch#conf t
Thu Jan 22 16:00:50 2026   MGMT-SW   Switch(config)#hostname MGMT-SW
Thu Jan 22 16:01:53 2026   MGMT-SW   MGMT-SW(config)#line con 0
Thu Jan 22 16:02:04 2026   MGMT-SW   MGMT-SW(config-line)#password CISEGCISCO
Thu Jan 22 16:02:16 2026   MGMT-SW   MGMT-SW(config-line)#login
Thu Jan 22 16:02:25 2026   MGMT-SW   MGMT-SW(config-line)#exit
Thu Jan 22 16:02:37 2026   MGMT-SW   MGMT-SW(config)#enable secret CISEGCISCO
Thu Jan 22 16:02:49 2026   MGMT-SW   MGMT-SW(config)#line vty 0 15
Thu Jan 22 16:03:00 2026   MGMT-SW   MGMT-SW(config-line)#password CISEGCISCO
Thu Jan 22 16:03:10 2026   MGMT-SW   MGMT-SW(config-line)#login
Thu Jan 22 16:03:19 2026   MGMT-SW   MGMT-SW(config-line)#exit
Thu Jan 22 16:03:45 2026   MGMT-SW   MGMT-SW(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 16:03:57 2026   MGMT-SW   MGMT-SW(config)#service password-encryption
Thu Jan 22 16:04:09 2026   MGMT-SW   MGMT-SW(config)#service timestamps log datetime msec
Thu Jan 22 16:04:22 2026   MGMT-SW   MGMT-SW(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 16:04:33 2026   MGMT-SW   MGMT-SW(config)#username admin secret CISEGCISCO
Thu Jan 22 16:04:45 2026   MGMT-SW   MGMT-SW(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 16:05:08 2026   MGMT-SW   MGMT-SW(config)#ip ssh version 2
Thu Jan 22 16:05:18 2026   MGMT-SW   MGMT-SW(config)#ip ssh time-out 90
Thu Jan 22 16:05:28 2026   MGMT-SW   MGMT-SW(config)#ip ssh authentication-retries 2
Thu Jan 22 16:05:39 2026   MGMT-SW   MGMT-SW(config)#line vty 0 15
Thu Jan 22 16:05:50 2026   MGMT-SW   MGMT-SW(config-line)#login local
Thu Jan 22 16:06:00 2026   MGMT-SW   MGMT-SW(config-line)#transport input ssh
Thu Jan 22 16:07:17 2026   MGMT-SW   MGMT-SW(config-line)#ip default-gateway 172.16.1.129
Thu Jan 22 16:07:31 2026   MGMT-SW   MGMT-SW(config)#interface vlan 1
Thu Jan 22 16:08:07 2026   MGMT-SW   MGMT-SW(config-if)#ip address 172.16.1.130 255.255.255.192
Thu Jan 22 16:08:14 2026   MGMT-SW   MGMT-SW(config-if)#no shut
Thu Jan 22 16:08:26 2026   MGMT-SW   MGMT-SW(config-if)#int g0/1
Thu Jan 22 16:08:47 2026   MGMT-SW   MGMT-SW(config-if)#description Ligacao ao router OPS-RTR-2
Thu Jan 22 16:08:51 2026   MGMT-SW   MGMT-SW(config-if)#no shut
Thu Jan 22 16:08:59 2026   MGMT-SW   MGMT-SW(config-if)#int f0/1
Thu Jan 22 16:09:23 2026   MGMT-SW   MGMT-SW(config-if)#description Ligacao ao PC NetAdmin
Thu Jan 22 16:09:28 2026   MGMT-SW   MGMT-SW(config-if)#no shut
Thu Jan 22 16:09:50 2026   MGMT-SW   MGMT-SW(config-if)#int f0/2
Thu Jan 22 16:10:23 2026   MGMT-SW   MGMT-SW(config-if)#description Ligacao ao servidor DC01
Thu Jan 22 16:10:26 2026   MGMT-SW   MGMT-SW(config-if)#no shut
Thu Jan 22 16:10:34 2026   MGMT-SW   MGMT-SW(config-if)#int f0/3
Thu Jan 22 16:10:52 2026   MGMT-SW   MGMT-SW(config-if)#description Ligacao ao servidor DC02
Thu Jan 22 16:10:57 2026   MGMT-SW   MGMT-SW(config-if)#no shut
Thu Jan 22 16:11:16 2026   MGMT-SW   MGMT-SW(config-if)#int range f0/4-24, g0/2
Thu Jan 22 16:11:19 2026   MGMT-SW   MGMT-SW(config-if-range)#shut
Thu Jan 22 16:11:26 2026   MGMT-SW   MGMT-SW(config-if-range)#end
Thu Jan 22 16:11:37 2026   MGMT-SW   MGMT-SW#copy run start
Thu Jan 22 16:20:51 2026   SERV-FARM-SW   Switch>ena
Thu Jan 22 16:20:53 2026   SERV-FARM-SW   Switch#conf t
Thu Jan 22 16:21:04 2026   SERV-FARM-SW   Switch(config)#hostname SERV-FARM-SW
Thu Jan 22 21:36:40 2026   SERV-FARM-SW   SERV-FARM-SW>ena
Thu Jan 22 21:36:42 2026   SERV-FARM-SW   SERV-FARM-SW#conf t
Thu Jan 22 21:36:46 2026   SERV-FARM-SW   SERV-FARM-SW(config)#line con 0
Thu Jan 22 21:36:55 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#password CISEGCISCO
Thu Jan 22 21:37:03 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#login
Thu Jan 22 21:37:06 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#exit
Thu Jan 22 21:37:16 2026   SERV-FARM-SW   SERV-FARM-SW(config)#enable secret CISEGCISCO
Thu Jan 22 21:37:25 2026   SERV-FARM-SW   SERV-FARM-SW(config)#line vty 0 15
Thu Jan 22 21:37:34 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#password CISEGCISCO
Thu Jan 22 21:37:37 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#login
Thu Jan 22 21:37:38 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#exit
Thu Jan 22 21:37:58 2026   SERV-FARM-SW   SERV-FARM-SW(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 21:38:11 2026   SERV-FARM-SW   SERV-FARM-SW(config)#service password-encryption
Thu Jan 22 21:38:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#service timestamps log datetime msec
Thu Jan 22 21:38:45 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 21:38:53 2026   SERV-FARM-SW   SERV-FARM-SW(config)#username admin secret CISEGCISCO
Thu Jan 22 21:39:05 2026   SERV-FARM-SW   SERV-FARM-SW(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 21:39:20 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ip ssh version 2
Thu Jan 22 21:39:28 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ip ssh time-out 90
Thu Jan 22 21:39:38 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ip ssh authentication-retries 2
Thu Jan 22 21:39:46 2026   SERV-FARM-SW   SERV-FARM-SW(config)#line vty 0 15
Thu Jan 22 21:39:54 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#login local
Thu Jan 22 21:40:02 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#transport input ssh
Thu Jan 22 21:40:35 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#ip default-gateway 172.16.1.193
Thu Jan 22 21:41:05 2026   SERV-FARM-SW   SERV-FARM-SW#conf t
Thu Jan 22 21:41:19 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ip default-gateway 172.16.1.193
Thu Jan 22 21:41:26 2026   SERV-FARM-SW   SERV-FARM-SW(config)#int vlan 1
Thu Jan 22 21:41:52 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#ip address 172.16.1.194 255.255.255.224
Thu Jan 22 21:42:00 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#no shut
Thu Jan 22 21:42:09 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#int g0/1
Thu Jan 22 21:42:32 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#description Ligacao ao router OPS-RTR-2
Thu Jan 22 21:42:36 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#no shut
Thu Jan 22 21:42:42 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#int f0/1
Thu Jan 22 21:43:00 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#description Ligacao ao servidor MODEL-1
Thu Jan 22 21:43:03 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#no shut
Thu Jan 22 21:43:08 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#int f0/2
Thu Jan 22 21:43:22 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#description Ligacao ao servidor MODEL-2
Thu Jan 22 21:43:25 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#no shut
Thu Jan 22 21:43:40 2026   SERV-FARM-SW   SERV-FARM-SW(config-if)#int range f0/3-24, g0/2
Thu Jan 22 21:43:42 2026   SERV-FARM-SW   SERV-FARM-SW(config-if-range)#shut
Thu Jan 22 21:43:59 2026   SERV-FARM-SW   SERV-FARM-SW(config-if-range)#end
Thu Jan 22 21:44:03 2026   SERV-FARM-SW   SERV-FARM-SW#copy run start
Thu Jan 22 21:45:21 2026   CORE-MLS-1   Switch>ena
Thu Jan 22 21:45:22 2026   CORE-MLS-1   Switch#conf t
Thu Jan 22 21:45:30 2026   CORE-MLS-1   Switch(config)#hostname CORE-MLS-1
Thu Jan 22 21:46:00 2026   CORE-MLS-1   CORE-MLS-1(config)#line con 0
Thu Jan 22 21:46:11 2026   CORE-MLS-1   CORE-MLS-1(config-line)#password CISEGCISCO
Thu Jan 22 21:46:14 2026   CORE-MLS-1   CORE-MLS-1(config-line)#login
Thu Jan 22 21:46:15 2026   CORE-MLS-1   CORE-MLS-1(config-line)#exit
Thu Jan 22 21:46:24 2026   CORE-MLS-1   CORE-MLS-1(config)#enable secret CISEGCISCO
Thu Jan 22 21:46:33 2026   CORE-MLS-1   CORE-MLS-1(config)#line vty 0 15
Thu Jan 22 21:46:41 2026   CORE-MLS-1   CORE-MLS-1(config-line)#password CISEGCISCO
Thu Jan 22 21:46:46 2026   CORE-MLS-1   CORE-MLS-1(config-line)#login
Thu Jan 22 21:46:47 2026   CORE-MLS-1   CORE-MLS-1(config-line)#exit
Thu Jan 22 21:47:05 2026   CORE-MLS-1   CORE-MLS-1(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 21:47:14 2026   CORE-MLS-1   CORE-MLS-1(config)#service password-encryption
Thu Jan 22 21:47:24 2026   CORE-MLS-1   CORE-MLS-1(config)#service timestamps log datetime msec
Thu Jan 22 21:47:33 2026   CORE-MLS-1   CORE-MLS-1(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 21:47:43 2026   CORE-MLS-1   CORE-MLS-1(config)#username admin secret CISEGCISCO
Thu Jan 22 21:47:53 2026   CORE-MLS-1   CORE-MLS-1(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 21:48:04 2026   CORE-MLS-1   CORE-MLS-1(config)#ip ssh version 2
Thu Jan 22 21:48:11 2026   CORE-MLS-1   CORE-MLS-1(config)#ip ssh time-out 90
Thu Jan 22 21:48:20 2026   CORE-MLS-1   CORE-MLS-1(config)#ip ssh authentication-retries 2
Thu Jan 22 21:48:28 2026   CORE-MLS-1   CORE-MLS-1(config)#line vty 0 15
Thu Jan 22 21:48:36 2026   CORE-MLS-1   CORE-MLS-1(config-line)#login local
Thu Jan 22 21:48:46 2026   CORE-MLS-1   CORE-MLS-1(config-line)#transport input ssh
Thu Jan 22 21:48:48 2026   CORE-MLS-1   CORE-MLS-1(config-line)#exit
Thu Jan 22 21:49:46 2026   CORE-MLS-1   CORE-MLS-1(config)#ip default-gateway 172.16.2.1
Thu Jan 22 21:49:59 2026   CORE-MLS-1   CORE-MLS-1(config)#int vlan 1
Thu Jan 22 21:54:04 2026   CORE-MLS-1   CORE-MLS-1(config-if)#ip address 172.16.2.4 255.255.255.248
Thu Jan 22 21:54:14 2026   CORE-MLS-1   CORE-MLS-1(config-if)#no shut
Thu Jan 22 21:54:19 2026   CORE-MLS-1   CORE-MLS-1(config-if)#exit
Thu Jan 22 21:54:36 2026   CORE-MLS-1   CORE-MLS-1(config)#int g1/0/1
Thu Jan 22 21:54:55 2026   CORE-MLS-1   CORE-MLS-1(config-if)#description Ligacao ao router CORE-EDGE
Thu Jan 22 21:54:59 2026   CORE-MLS-1   CORE-MLS-1(config-if)#no shut
Thu Jan 22 21:55:17 2026   CORE-MLS-1   CORE-MLS-1(config-if)#int g1/0/2
Thu Jan 22 21:55:29 2026   CORE-MLS-1   CORE-MLS-1(config-if)#description Ligacao ao ENT-ADM-MLS
Thu Jan 22 21:55:32 2026   CORE-MLS-1   CORE-MLS-1(config-if)#no shut
Thu Jan 22 21:55:48 2026   CORE-MLS-1   CORE-MLS-1(config-if)#int g1/0/3
Thu Jan 22 21:56:04 2026   CORE-MLS-1   CORE-MLS-1(config-if)#description Ligacao ao router OPS-RTR-1
Thu Jan 22 21:56:06 2026   CORE-MLS-1   CORE-MLS-1(config-if)#no shut
Thu Jan 22 21:57:25 2026   CORE-MLS-1   CORE-MLS-1(config-if)#int range g1/0/4-24, g1/1/1-4
Thu Jan 22 21:57:27 2026   CORE-MLS-1   CORE-MLS-1(config-if-range)#shut
Thu Jan 22 21:57:55 2026   CORE-MLS-1   CORE-MLS-1(config-if-range)#end
Thu Jan 22 21:58:00 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Thu Jan 22 22:02:41 2026   ENT-ADM-MLS   Switch>ena
Thu Jan 22 22:02:43 2026   ENT-ADM-MLS   Switch#conf t
Thu Jan 22 22:02:55 2026   ENT-ADM-MLS   Switch(config)#hostname ENT-ADM-MLS
Thu Jan 22 22:10:18 2026   CORE-MLS-1   CORE-MLS-1>ENA
Thu Jan 22 22:10:26 2026   CORE-MLS-1   CORE-MLS-1#conf t
Thu Jan 22 22:10:48 2026   CORE-MLS-1   CORE-MLS-1(config)#login block-for 90 attempts 2 within 10
Thu Jan 22 22:10:50 2026   CORE-MLS-1   CORE-MLS-1(config)#end
Thu Jan 22 22:10:55 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Thu Jan 22 22:23:54 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Thu Jan 22 22:23:56 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Thu Jan 22 22:24:43 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#line con 0
Thu Jan 22 22:24:53 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#password CISEGCISCO
Thu Jan 22 22:24:56 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#login
Thu Jan 22 22:24:58 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#exit
Thu Jan 22 22:25:08 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#enable secret CISEGCISCO
Thu Jan 22 22:25:20 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#line vty 0 15
Thu Jan 22 22:25:29 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#password CISEGCISCO
Thu Jan 22 22:25:34 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#login
Thu Jan 22 22:25:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#exit
Thu Jan 22 22:25:56 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 22:26:05 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#service password-encryption
Thu Jan 22 22:26:14 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#login block-for 90 attempts 2 within 10
Thu Jan 22 22:26:25 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#security passwords min-length 10
Thu Jan 22 22:26:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#service timestamps log datetime msec
Thu Jan 22 22:26:49 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 22:26:57 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#username admin secret CISEGCISCO
Thu Jan 22 22:27:07 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 22:27:15 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip ssh version 2
Thu Jan 22 22:27:26 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip ssh time-out 90
Thu Jan 22 22:27:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip ssh authentication-retries 2
Thu Jan 22 22:27:43 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#line vty 0 15
Thu Jan 22 22:27:52 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#login local
Thu Jan 22 22:28:00 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#transport input ssh
Thu Jan 22 22:28:05 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#exit
Thu Jan 22 22:31:04 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip routing
Thu Jan 22 22:31:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#int g1/0/1
Thu Jan 22 22:31:48 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#no switchport
Thu Jan 22 22:32:56 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip address 172.16.2.3 255.255.255.248
Thu Jan 22 22:33:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#description Ligacao ao CORE-MLS-1
Thu Jan 22 22:36:32 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#no shut
Thu Jan 22 22:37:40 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#exit
Thu Jan 22 22:37:51 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vlan 10
Thu Jan 22 22:38:19 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#name Development
Thu Jan 22 22:38:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#vlan 20
Thu Jan 22 22:38:46 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#name Accounting
Thu Jan 22 22:39:01 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#vlan 30
Thu Jan 22 22:39:15 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#name Consulting
Thu Jan 22 22:39:27 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#vlan 40
Thu Jan 22 22:39:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#name Management
Thu Jan 22 22:40:20 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#int vlan 10
Thu Jan 22 22:43:54 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip address 172.16.10.1 255.255.254.0
Thu Jan 22 22:44:04 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#int vlan 20
Thu Jan 22 22:44:52 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip address 172.16.20.1 255.255.255.128
Thu Jan 22 22:45:12 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#int vlan 30
Thu Jan 22 22:45:50 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip address 172.16.30.1 255.255.255.192
Thu Jan 22 22:45:59 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#int vlan 40
Thu Jan 22 22:46:49 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip address 172.16.40.1 255.255.255.224
Thu Jan 22 22:49:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#int range g1/0/2-3
Thu Jan 22 22:49:56 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#switchport mode trunk
Thu Jan 22 22:50:25 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#switchport trunk allowed vlan 10,20,30,40
Thu Jan 22 22:50:49 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#switchport trunk native vlan 40
Thu Jan 22 22:51:06 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#exit
Thu Jan 22 22:51:27 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vtp mode ?
Thu Jan 22 22:51:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vtp mode server
Thu Jan 22 22:51:45 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vtp version 2
Thu Jan 22 22:52:02 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vtp domain qwertycorp
Thu Jan 22 22:52:26 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vtp password CISEGCISCO
Thu Jan 22 22:57:01 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#end
Thu Jan 22 22:57:04 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Thu Jan 22 22:57:54 2026   ADM-SW-1   Switch>enable
Thu Jan 22 22:57:54 2026   ADM-SW-1   Switch#configure terminal
Thu Jan 22 22:57:54 2026   ADM-SW-1   Switch(config)#interface GigabitEthernet0/1
Thu Jan 22 22:58:06 2026   ADM-SW-2   Switch>enable
Thu Jan 22 22:58:06 2026   ADM-SW-2   Switch#configure terminal
Thu Jan 22 22:58:06 2026   ADM-SW-2   Switch(config)#interface GigabitEthernet0/2
Thu Jan 22 22:58:10 2026   ADM-SW-2   Switch(config-if)#exit
Thu Jan 22 22:58:10 2026   ADM-SW-2   Switch(config)#interface GigabitEthernet0/1
Thu Jan 22 23:07:44 2026   ADM-SW-1   Switch(config-if)#exit
Thu Jan 22 23:07:58 2026   ADM-SW-1   Switch(config)#hostname ADM-SW-1
Thu Jan 22 23:08:43 2026   ADM-SW-1   ADM-SW-1(config)#line con 0
Thu Jan 22 23:08:52 2026   ADM-SW-1   ADM-SW-1(config-line)#password CISEGCISCO
Thu Jan 22 23:08:58 2026   ADM-SW-1   ADM-SW-1(config-line)#login
Thu Jan 22 23:09:01 2026   ADM-SW-1   ADM-SW-1(config-line)#exit
Thu Jan 22 23:09:09 2026   ADM-SW-1   ADM-SW-1(config)#enable secret CISEGCISCO
Thu Jan 22 23:09:19 2026   ADM-SW-1   ADM-SW-1(config)#line vty 0 15
Thu Jan 22 23:09:27 2026   ADM-SW-1   ADM-SW-1(config-line)#password CISEGCISCO
Thu Jan 22 23:09:30 2026   ADM-SW-1   ADM-SW-1(config-line)#login
Thu Jan 22 23:09:32 2026   ADM-SW-1   ADM-SW-1(config-line)#exit
Thu Jan 22 23:09:53 2026   ADM-SW-1   ADM-SW-1(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 23:10:04 2026   ADM-SW-1   ADM-SW-1(config)#service password-encryption
Thu Jan 22 23:10:14 2026   ADM-SW-1   ADM-SW-1(config)#service timestamps log datetime msec
Thu Jan 22 23:10:25 2026   ADM-SW-1   ADM-SW-1(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 23:10:34 2026   ADM-SW-1   ADM-SW-1(config)#username admin secret CISEGCISCO
Thu Jan 22 23:10:44 2026   ADM-SW-1   ADM-SW-1(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 23:10:57 2026   ADM-SW-1   ADM-SW-1(config)#ip ssh version 2
Thu Jan 22 23:11:07 2026   ADM-SW-1   ADM-SW-1(config)#ip ssh time-out 90
Thu Jan 22 23:11:16 2026   ADM-SW-1   ADM-SW-1(config)#ip ssh authentication-retries 2
Thu Jan 22 23:11:24 2026   ADM-SW-1   ADM-SW-1(config)#line vty 0 15
Thu Jan 22 23:11:32 2026   ADM-SW-1   ADM-SW-1(config-line)#login local
Thu Jan 22 23:11:40 2026   ADM-SW-1   ADM-SW-1(config-line)#transport input ssh
Thu Jan 22 23:12:31 2026   ADM-SW-1   ADM-SW-1(config-line)#exit
Thu Jan 22 23:12:35 2026   ADM-SW-1   ADM-SW-1(config)#vtp mode client
Thu Jan 22 23:12:44 2026   ADM-SW-1   ADM-SW-1(config)#vtp version 2
Thu Jan 22 23:13:10 2026   ADM-SW-1   ADM-SW-1(config)#vtp password CISEGCISCO
Thu Jan 22 23:13:32 2026   ADM-SW-1   ADM-SW-1(config)#vtp domain qwertycorp
Thu Jan 22 23:13:47 2026   ADM-SW-1   ADM-SW-1(config)#do sh vlan
Thu Jan 22 23:14:35 2026   ADM-SW-1   ADM-SW-1(config)#int g0/1
Thu Jan 22 23:14:50 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport mode trunk
Thu Jan 22 23:15:29 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport trunk allowed vlan 10,20,30,40
Thu Jan 22 23:16:01 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport trunk native vlan 40
Thu Jan 22 23:16:39 2026   ADM-SW-1   ADM-SW-1(config-if)#exit
Thu Jan 22 23:16:44 2026   ADM-SW-1   ADM-SW-1(config)#int vlan 10
Thu Jan 22 23:16:49 2026   ADM-SW-1   ADM-SW-1(config-if)#int vlan 20
Thu Jan 22 23:16:54 2026   ADM-SW-1   ADM-SW-1(config-if)#int vlan 30
Thu Jan 22 23:16:58 2026   ADM-SW-1   ADM-SW-1(config-if)#int vlan 40
Thu Jan 22 23:18:24 2026   ADM-SW-1   ADM-SW-1(config-if)#ip address 172.16.40.2 255.255.255.224
Thu Jan 22 23:19:14 2026   ADM-SW-1   ADM-SW-1(config-if)#exit
Thu Jan 22 23:19:25 2026   ADM-SW-1   ADM-SW-1(config)#ip default-gateway 172.16.40.1
Thu Jan 22 23:20:19 2026   ADM-SW-1   ADM-SW-1(config)#int f0/1
Thu Jan 22 23:20:45 2026   ADM-SW-1   ADM-SW-1(config-if)#description Ligacao ao PC5
Thu Jan 22 23:20:47 2026   ADM-SW-1   ADM-SW-1(config-if)#no shut
Thu Jan 22 23:21:36 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport mode access
Thu Jan 22 23:22:02 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport access vlan 10
Thu Jan 22 23:22:18 2026   ADM-SW-1   ADM-SW-1(config-if)#int f0/2
Thu Jan 22 23:22:57 2026   ADM-SW-1   ADM-SW-1(config-if)#description Ligacao a PT-F1
Thu Jan 22 23:23:11 2026   ADM-SW-1   ADM-SW-1(config-if)#no shut
Thu Jan 22 23:23:26 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport mode access
Thu Jan 22 23:23:36 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport access vlan 40
Thu Jan 22 23:24:03 2026   ADM-SW-1   ADM-SW-1(config-if)#int f0/3
Thu Jan 22 23:24:16 2026   ADM-SW-1   ADM-SW-1(config-if)#description Ligacao ao PC6
Thu Jan 22 23:24:19 2026   ADM-SW-1   ADM-SW-1(config-if)#no shut
Thu Jan 22 23:24:36 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport mode access
Thu Jan 22 23:24:53 2026   ADM-SW-1   ADM-SW-1(config-if)#switchport access vlan 20
Thu Jan 22 23:33:38 2026   ENT-ADM-MLS   ENT-ADM-MLS>ENA
Thu Jan 22 23:33:54 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Thu Jan 22 23:34:02 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#vlan 5
Thu Jan 22 23:34:06 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#name LOCK
Thu Jan 22 23:34:43 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-vlan)#int vlan 5
Thu Jan 22 23:35:13 2026   ADM-SW-1   ADM-SW-1(config-if)#exit
Thu Jan 22 23:36:23 2026   ADM-SW-1   ADM-SW-1(config)#int range f0/4-24, g0/2
Thu Jan 22 23:36:42 2026   ADM-SW-1   ADM-SW-1(config-if-range)#switchport mode access
Thu Jan 22 23:36:51 2026   ADM-SW-1   ADM-SW-1(config-if-range)#switchport access vlan 5
Thu Jan 22 23:36:55 2026   ADM-SW-1   ADM-SW-1(config-if-range)#shut
Thu Jan 22 23:37:12 2026   ADM-SW-1   ADM-SW-1(config-if-range)#end
Thu Jan 22 23:37:16 2026   ADM-SW-1   ADM-SW-1#copy run start
Thu Jan 22 23:38:34 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#exit
Thu Jan 22 23:39:18 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#int range g1/0/4-24, g1/1/1-4
Thu Jan 22 23:39:20 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#shut
Thu Jan 22 23:39:25 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if-range)#end
Thu Jan 22 23:39:29 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Thu Jan 22 23:39:57 2026   ADM-SW-2   Switch>ena
Thu Jan 22 23:39:59 2026   ADM-SW-2   Switch#conf t
Thu Jan 22 23:40:07 2026   ADM-SW-2   Switch(config)#hostname ADM-SW-2
Thu Jan 22 23:41:09 2026   ADM-SW-2   ADM-SW-2(config)#line con 0
Thu Jan 22 23:41:17 2026   ADM-SW-2   ADM-SW-2(config-line)#password CISEGCISCO
Thu Jan 22 23:41:21 2026   ADM-SW-2   ADM-SW-2(config-line)#login
Thu Jan 22 23:41:22 2026   ADM-SW-2   ADM-SW-2(config-line)#exit
Thu Jan 22 23:41:31 2026   ADM-SW-2   ADM-SW-2(config)#enable secret CISEGCISCO
Thu Jan 22 23:41:40 2026   ADM-SW-2   ADM-SW-2(config)#line vty 0 15
Thu Jan 22 23:41:48 2026   ADM-SW-2   ADM-SW-2(config-line)#password CISEGCISCO
Thu Jan 22 23:41:52 2026   ADM-SW-2   ADM-SW-2(config-line)#login
Thu Jan 22 23:41:53 2026   ADM-SW-2   ADM-SW-2(config-line)#exit
Thu Jan 22 23:42:18 2026   ADM-SW-2   ADM-SW-2(config)#banner motd "This equipment belongs to QWERTYCorp. Any unauthorized attempt to access it will be considered a violation with legal consequences."
Thu Jan 22 23:42:31 2026   ADM-SW-2   ADM-SW-2(config)#service password-encryption
Thu Jan 22 23:42:39 2026   ADM-SW-2   ADM-SW-2(config)#service timestamps log datetime msec
Thu Jan 22 23:42:47 2026   ADM-SW-2   ADM-SW-2(config)#ip domain-name QWERTYCorp.org
Thu Jan 22 23:42:54 2026   ADM-SW-2   ADM-SW-2(config)#username admin secret CISEGCISCO
Thu Jan 22 23:43:03 2026   ADM-SW-2   ADM-SW-2(config)#crypto key generate rsa general-keys modulus 1024
Thu Jan 22 23:43:18 2026   ADM-SW-2   ADM-SW-2(config)#ip ssh version 2
Thu Jan 22 23:43:25 2026   ADM-SW-2   ADM-SW-2(config)#ip ssh time-out 90
Thu Jan 22 23:43:33 2026   ADM-SW-2   ADM-SW-2(config)#ip ssh authentication-retries 2
Thu Jan 22 23:43:40 2026   ADM-SW-2   ADM-SW-2(config)#line vty 0 15
Thu Jan 22 23:43:48 2026   ADM-SW-2   ADM-SW-2(config-line)#login local
Thu Jan 22 23:43:57 2026   ADM-SW-2   ADM-SW-2(config-line)#transport input ssh
Thu Jan 22 23:44:20 2026   ADM-SW-2   ADM-SW-2(config-line)#exit
Thu Jan 22 23:44:49 2026   ADM-SW-2   ADM-SW-2(config)#vtp mode client
Thu Jan 22 23:44:53 2026   ADM-SW-2   ADM-SW-2(config)#vtp version 2
Thu Jan 22 23:45:08 2026   ADM-SW-2   ADM-SW-2(config)#vtp domain qwertycorp
Thu Jan 22 23:45:20 2026   ADM-SW-2   ADM-SW-2(config)#vtp password CISEGCISCO
Thu Jan 22 23:45:38 2026   ADM-SW-2   ADM-SW-2(config)#int g0/1
Thu Jan 22 23:45:53 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport mode trunk
Thu Jan 22 23:46:08 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport trunk allowed 10,20,30,40
Thu Jan 22 23:46:19 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport trunk allowed vlan 10,20,30,40
Thu Jan 22 23:46:39 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport trunk native vlan 40
Thu Jan 22 23:46:58 2026   ADM-SW-2   ADM-SW-2(config-if)#exit
Thu Jan 22 23:48:02 2026   ADM-SW-2   ADM-SW-2(config)#int range f0/1
Thu Jan 22 23:48:07 2026   ADM-SW-2   ADM-SW-2(config-if-range)#exit
Thu Jan 22 23:48:12 2026   ADM-SW-2   ADM-SW-2(config)#int f0/1
Thu Jan 22 23:48:20 2026   ADM-SW-2   ADM-SW-2(config-if)#no shut
Thu Jan 22 23:48:45 2026   ADM-SW-2   ADM-SW-2(config-if)#description Ligacao ao PC7
Thu Jan 22 23:48:59 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport mode access
Thu Jan 22 23:49:16 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport access vlan 30
Thu Jan 22 23:49:30 2026   ADM-SW-2   ADM-SW-2(config-if)#int f0/2
Thu Jan 22 23:49:33 2026   ADM-SW-2   ADM-SW-2(config-if)#no shut
Thu Jan 22 23:49:56 2026   ADM-SW-2   ADM-SW-2(config-if)#description Ligacao a PT-F2
Thu Jan 22 23:50:02 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport mode access
Thu Jan 22 23:50:12 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport access vlan 40
Thu Jan 22 23:50:19 2026   ADM-SW-2   ADM-SW-2(config-if)#int f0/3
Thu Jan 22 23:50:22 2026   ADM-SW-2   ADM-SW-2(config-if)#no shut
Thu Jan 22 23:50:36 2026   ADM-SW-2   ADM-SW-2(config-if)#description Ligacao ao PC8
Thu Jan 22 23:50:39 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport mode access
Thu Jan 22 23:50:44 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport access vlan 40
Thu Jan 22 23:50:51 2026   ADM-SW-2   ADM-SW-2(config-if)#int f0/4
Thu Jan 22 23:50:53 2026   ADM-SW-2   ADM-SW-2(config-if)#no shut
Thu Jan 22 23:51:10 2026   ADM-SW-2   ADM-SW-2(config-if)#description Ligacao ao servidor NAS-1
Thu Jan 22 23:51:16 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport mode access
Thu Jan 22 23:51:19 2026   ADM-SW-2   ADM-SW-2(config-if)#switchport access vlan 40
Thu Jan 22 23:52:55 2026   ADM-SW-2   ADM-SW-2(config-if)#exit
Thu Jan 22 23:53:15 2026   ADM-SW-2   ADM-SW-2(config)#int range f0/5-24, g0/2
Thu Jan 22 23:53:24 2026   ADM-SW-2   ADM-SW-2(config-if-range)#switchport mode access
Thu Jan 22 23:53:36 2026   ADM-SW-2   ADM-SW-2(config-if-range)#switchport access vlan 5
Thu Jan 22 23:53:38 2026   ADM-SW-2   ADM-SW-2(config-if-range)#shut
Thu Jan 22 23:53:47 2026   ADM-SW-2   ADM-SW-2(config-if-range)#end
Thu Jan 22 23:53:51 2026   ADM-SW-2   ADM-SW-2#copy run start
Thu Jan 22 23:56:44 2026   ADM-SW-2   ADM-SW-2#conf t
Thu Jan 22 23:56:49 2026   ADM-SW-2   ADM-SW-2(config)#int vlan 10
Thu Jan 22 23:56:54 2026   ADM-SW-2   ADM-SW-2(config-if)#int vlan 20
Thu Jan 22 23:56:58 2026   ADM-SW-2   ADM-SW-2(config-if)#int vlan 30
Thu Jan 22 23:57:05 2026   ADM-SW-2   ADM-SW-2(config-if)#int vlan 40
Thu Jan 22 23:57:23 2026   ADM-SW-2   ADM-SW-2(config-if)#ip address 172.16.40.3 255.255.255.224
Thu Jan 22 23:57:34 2026   ADM-SW-2   ADM-SW-2(config-if)#exit
Thu Jan 22 23:57:47 2026   ADM-SW-2   ADM-SW-2(config)#ip default-gateway 172.16.40.1
Thu Jan 22 23:58:33 2026   ADM-SW-2   ADM-SW-2(config)#end
Thu Jan 22 23:58:36 2026   ADM-SW-2   ADM-SW-2#copy run start
Sun Jan 25 12:55:14 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Sun Jan 25 12:55:28 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Sun Jan 25 13:03:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp excluded-address 172.16.10.0 172.16.10.20
Sun Jan 25 13:03:41 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp excluded-address 172.16.20.0 172.16.20.20
Sun Jan 25 13:04:28 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp excluded-address 172.16.30.0 172.16.30.20
Sun Jan 25 13:06:45 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp pool POOLVLAN10
Sun Jan 25 13:09:22 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#network 172.16.10.0 255.255.254.0
Sun Jan 25 13:10:21 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#default-router 172.16.10.1
Sun Jan 25 13:11:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#dns-server 172.16.1.12
Sun Jan 25 13:11:20 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#domain-name qwertycorp.org
Sun Jan 25 13:11:29 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#exit
Sun Jan 25 13:12:45 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp pool POOLVLAN20
Sun Jan 25 13:13:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#network 172.16.20.0 255.255.255.128
Sun Jan 25 13:13:53 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#default-router 172.16.20.1
Sun Jan 25 13:13:59 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#dns-server 172.16.1.12
Sun Jan 25 13:14:12 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#domain-name qwertycorp.org
Sun Jan 25 13:14:27 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#exit
Sun Jan 25 13:16:27 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ip dhcp pool POOLVLAN30
Sun Jan 25 13:17:16 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#network 172.16.30.0 255.255.255.192
Sun Jan 25 13:20:30 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#default-router 172.16.30.1
Sun Jan 25 13:20:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#dns-server 172.16.1.12
Sun Jan 25 13:20:47 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#domain-name qwertycorp.org
Sun Jan 25 13:21:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(dhcp-config)#exit
Sun Jan 25 13:23:35 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#end
Sun Jan 25 13:23:39 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Sun Jan 25 15:51:27 2026   OPS-RTR-1   OPS-RTR-1>ENA
Sun Jan 25 15:51:32 2026   OPS-RTR-1   OPS-RTR-1#CONF T
Sun Jan 25 15:53:58 2026   OPS-RTR-1   OPS-RTR-1(config)#ip dhcp excluded-address 172.16.0.0 172.16.0.20
Sun Jan 25 15:54:39 2026   OPS-RTR-1   OPS-RTR-1(config)#ip dhcp pool POOLSOC
Sun Jan 25 15:55:05 2026   OPS-RTR-1   OPS-RTR-1(dhcp-config)#network 172.16.0.0 255.255.255.0
Sun Jan 25 15:55:19 2026   OPS-RTR-1   OPS-RTR-1(dhcp-config)#default-router 172.16.0.1
Sun Jan 25 15:55:31 2026   OPS-RTR-1   OPS-RTR-1(dhcp-config)#dns-server 172.16.1.12
Sun Jan 25 15:58:10 2026   OPS-RTR-1   OPS-RTR-1(dhcp-config)#domain-name qwertycorp.org
Sun Jan 25 15:59:11 2026   OPS-RTR-1   OPS-RTR-1(dhcp-config)#end
Sun Jan 25 15:59:16 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Sun Jan 25 15:59:35 2026   BRANCH-1   BRANCH-1>ENA
Sun Jan 25 15:59:42 2026   BRANCH-1   BRANCH-1#conf t
Sun Jan 25 16:03:19 2026   BRANCH-1   BRANCH-1(config)#ip dhcp excluded-address 172.24.0.0 172.24.0.20
Sun Jan 25 16:03:50 2026   BRANCH-1   BRANCH-1(config)#ip dhcp pool POOLBRANCH
Sun Jan 25 16:04:05 2026   BRANCH-1   BRANCH-1(dhcp-config)#network 172.24.0.0 255.255.255.0
Sun Jan 25 16:04:28 2026   BRANCH-1   BRANCH-1(dhcp-config)#default-router 172.24.0.1
Sun Jan 25 16:20:17 2026   BRANCH-1   BRANCH-1>ENA
Sun Jan 25 16:20:24 2026   BRANCH-1   BRANCH-1#conf t
Sun Jan 25 16:20:42 2026   BRANCH-1   BRANCH-1(config)#ip dhcp pool POOLBRANCH
Sun Jan 25 16:20:59 2026   BRANCH-1   BRANCH-1(dhcp-config)#dns-server 172.16.1.12
Sun Jan 25 16:22:15 2026   BRANCH-1   BRANCH-1(dhcp-config)#domain-name qwertycorp.org
Sun Jan 25 16:22:28 2026   BRANCH-1   BRANCH-1(dhcp-config)#end
Sun Jan 25 16:22:36 2026   BRANCH-1   BRANCH-1#copy run start
Sun Jan 25 16:34:33 2026   ENT-ADM-MLS   ENT-ADM-MLS>ENA
Sun Jan 25 16:34:48 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Sun Jan 25 16:36:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#key chain SECURE-OSPF
Sun Jan 25 16:36:39 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-keychain)#key 1
Sun Jan 25 16:39:34 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-keychain-key)#key-string CISEGCISCO
Sun Jan 25 16:40:09 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-keychain-key)#cryptographic-algorithm hmac-sha-256
Sun Jan 25 16:41:53 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-keychain-key)#?
Sun Jan 25 20:04:49 2026   ENT-ADM-MLS   ENT-ADM-MLS>ENA
Sun Jan 25 20:05:10 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ?
Sun Jan 25 20:05:26 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh 
Sun Jan 25 20:05:32 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ?
Sun Jan 25 20:05:39 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ip ?
Sun Jan 25 20:05:47 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ip ospf
Sun Jan 25 20:06:21 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Sun Jan 25 23:23:46 2026   CORE-EDGE   CORE-EDGE>ENA
Sun Jan 25 23:23:52 2026   CORE-EDGE   CORE-EDGE#conf t
Sun Jan 25 23:25:11 2026   CORE-EDGE   CORE-EDGE(config)#router ospf 10
Sun Jan 25 23:25:11 2026   CORE-EDGE   CORE-EDGE(config-router)#area 0 authentication message-digest
Sun Jan 25 23:25:11 2026   CORE-EDGE   CORE-EDGE(config-router)#int g0/0/1
Sun Jan 25 23:25:11 2026   CORE-EDGE   CORE-EDGE(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Sun Jan 25 23:25:13 2026   CORE-EDGE   CORE-EDGE(config-if)#ip ospf authentication message-digest
Sun Jan 25 23:26:31 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Sun Jan 25 23:27:45 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Sun Jan 25 23:27:50 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Sun Jan 25 23:28:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#router ospf 10
Sun Jan 25 23:28:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#area 0 authentication message-digest
Sun Jan 25 23:28:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#int g1/0/1
Sun Jan 25 23:28:42 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Sun Jan 25 23:28:48 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#ip ospf authentication message-digest
Sun Jan 25 23:28:51 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-if)#exit
Sun Jan 25 23:29:20 2026   OPS-RTR-1   OPS-RTR-1>ena
Sun Jan 25 23:29:30 2026   OPS-RTR-1   OPS-RTR-1#conf t
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config)#router ospf 10
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-router)#area 0 authentication message-digest
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-router)#int g0/0/1
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf authentication message-digest
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-if)#int s0/1/0
Sun Jan 25 23:31:06 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Sun Jan 25 23:31:12 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf authentication message-digest
Sun Jan 25 23:31:14 2026   OPS-RTR-1   OPS-RTR-1(config-if)#exit
Sun Jan 25 23:32:04 2026   OPS-RTR-2   OPS-RTR-2>ENA
Sun Jan 25 23:32:10 2026   OPS-RTR-2   OPS-RTR-2#conf t
Sun Jan 25 23:32:12 2026   OPS-RTR-2   OPS-RTR-2(config)#router ospf 10
Sun Jan 25 23:32:12 2026   OPS-RTR-2   OPS-RTR-2(config-router)#area 0 authentication message-digest
Sun Jan 25 23:32:12 2026   OPS-RTR-2   OPS-RTR-2(config-router)#int s0/1/0
Sun Jan 25 23:32:12 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Sun Jan 25 23:32:15 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip ospf authentication message-digest
Sun Jan 25 23:32:18 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Sun Jan 25 23:33:24 2026   CORE-EDGE   CORE-EDGE(config)#router ospf 10
Sun Jan 25 23:33:35 2026   CORE-EDGE   CORE-EDGE(config-router)#router-id 4.4.4.4
Sun Jan 25 23:34:22 2026   CORE-EDGE   CORE-EDGE(config-router)#network 172.16.1.0 0.0.0.127 area 0
Sun Jan 25 23:35:58 2026   CORE-EDGE   CORE-EDGE(config-router)#network 172.16.2.0 0.0.0.7 area 0
Sun Jan 25 23:37:09 2026   CORE-EDGE   CORE-EDGE(config-router)#passive-interface g0/0/2
Sun Jan 25 23:37:18 2026   CORE-EDGE   CORE-EDGE(config-router)#default-information originate
Sun Jan 25 23:37:23 2026   CORE-EDGE   CORE-EDGE(config-router)#exit
Sun Jan 25 23:37:45 2026   CORE-EDGE   CORE-EDGE(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.254
Sun Jan 25 23:38:07 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/1
Sun Jan 25 23:38:18 2026   CORE-EDGE   CORE-EDGE(config-if)#ip ospf priority 255
Sun Jan 25 23:38:22 2026   CORE-EDGE   CORE-EDGE(config-if)#end
Sun Jan 25 23:38:28 2026   CORE-EDGE   CORE-EDGE#copy run start
Sun Jan 25 23:39:38 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#router ospf 10
Sun Jan 25 23:39:50 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#router-id 2.2.2.2
Sun Jan 25 23:41:11 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#network 172.16.10.0 0.0.1.255 area 0
Sun Jan 25 23:41:52 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#network 172.16.20.0 0.0.0.127 area 0
Sun Jan 25 23:43:10 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#network 172.16.30.0 0.0.0.63 area 0
Sun Jan 25 23:44:06 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#network 172.16.40.0 0.0.0.31 area 0
Sun Jan 25 23:45:01 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#network 172.16.2.0 0.0.0.7 area 0
Sun Jan 25 23:45:33 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#passive-interface vlan 10
Sun Jan 25 23:45:36 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#passive-interface vlan 20
Sun Jan 25 23:45:39 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#passive-interface vlan 30
Sun Jan 25 23:45:45 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#passive-interface vlan 40
Sun Jan 25 23:46:20 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-router)#end
Sun Jan 25 23:46:28 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Sun Jan 25 23:47:17 2026   OPS-RTR-1   OPS-RTR-1>ena
Sun Jan 25 23:47:22 2026   OPS-RTR-1   OPS-RTR-1#conf t
Sun Jan 25 23:47:57 2026   OPS-RTR-1   OPS-RTR-1(config)#router ospf 10
Sun Jan 25 23:48:07 2026   OPS-RTR-1   OPS-RTR-1(config-router)#router-id 3.3.3.3
Sun Jan 25 23:49:04 2026   OPS-RTR-1   OPS-RTR-1(config-router)#network 172.16.2.0 0.0.0.7 area 0
Sun Jan 25 23:50:00 2026   OPS-RTR-1   OPS-RTR-1(config-router)#network 172.16.0.0 0.0.0.255 area 0
Sun Jan 25 23:50:27 2026   OPS-RTR-1   OPS-RTR-1(config-router)#network 172.16.1.224 0.0.0.3 area 0
Sun Jan 25 23:51:17 2026   OPS-RTR-1   OPS-RTR-1(config-router)#passive-interface g0/0/1
Sun Jan 25 23:51:40 2026   OPS-RTR-1   OPS-RTR-1(config-router)#int s0/1/0
Sun Jan 25 23:51:55 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf network pointo-to-point
Sun Jan 25 23:52:02 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf network point-to-point
Sun Jan 25 23:52:26 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf hello-interval 20
Sun Jan 25 23:52:43 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf dead-interval 80
Sun Jan 25 23:53:01 2026   OPS-RTR-1   OPS-RTR-1(config-if)#int g0/0/0
Sun Jan 25 23:53:12 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf priority 128
Sun Jan 25 23:53:16 2026   OPS-RTR-1   OPS-RTR-1(config-if)#end
Sun Jan 25 23:53:20 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Sun Jan 25 23:54:21 2026   OPS-RTR-2   OPS-RTR-2>ena
Sun Jan 25 23:54:32 2026   OPS-RTR-2   OPS-RTR-2#conf t
Sun Jan 25 23:55:22 2026   OPS-RTR-2   OPS-RTR-2(config)#router ospf 10
Sun Jan 25 23:55:30 2026   OPS-RTR-2   OPS-RTR-2(config-router)#router-id 1.1.1.1
Sun Jan 25 23:56:51 2026   OPS-RTR-2   OPS-RTR-2(config-router)#network 172.16.1.224 0.0.0.3 area 0
Sun Jan 25 23:57:47 2026   OPS-RTR-2   OPS-RTR-2(config-router)#network 172.16.1.128 0.0.0.63 area 0
Sun Jan 25 23:58:20 2026   OPS-RTR-2   OPS-RTR-2(config-router)#network 172.16.1.192 0.0.0.31 area 0
Sun Jan 25 23:58:59 2026   OPS-RTR-2   OPS-RTR-2(config-router)#passive-interface g0/0/0
Sun Jan 25 23:59:09 2026   OPS-RTR-2   OPS-RTR-2(config-router)#passive-interface g0/0/1
Sun Jan 25 23:59:40 2026   OPS-RTR-2   OPS-RTR-2(config-router)#int s0/1/0
Sun Jan 25 23:59:53 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip ospf network point-to-point
Mon Jan 26 00:00:04 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip
Mon Jan 26 00:00:16 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip ospf hello-interval 20
Mon Jan 26 00:00:28 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip ospf dead-interval 80
Mon Jan 26 00:00:41 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Mon Jan 26 00:00:53 2026   OPS-RTR-2   OPS-RTR-2(config)#do sh ip ospf ne
Mon Jan 26 00:01:00 2026   OPS-RTR-2   OPS-RTR-2(config)#end
Mon Jan 26 00:01:05 2026   OPS-RTR-2   OPS-RTR-2#copy run start
Mon Jan 26 00:01:24 2026   OPS-RTR-1   OPS-RTR-1#sh ip ospf ne
Mon Jan 26 00:02:25 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Mon Jan 26 00:02:36 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ip ospf ne
Mon Jan 26 00:03:44 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 00:03:52 2026   CORE-EDGE   CORE-EDGE#sh ip ospf ne
Mon Jan 26 00:19:38 2026   OPS-RTR-2   OPS-RTR-2>ena
Mon Jan 26 00:19:42 2026   OPS-RTR-2   OPS-RTR-2#conf t
Mon Jan 26 00:20:20 2026   OPS-RTR-2   OPS-RTR-2(config)#exiyt
Mon Jan 26 00:20:23 2026   OPS-RTR-2   OPS-RTR-2(config)#exit
Mon Jan 26 00:20:28 2026   OPS-RTR-2   OPS-RTR-2#clear ip ospf process
Mon Jan 26 00:21:00 2026   OPS-RTR-1   OPS-RTR-1>ena
Mon Jan 26 00:21:06 2026   OPS-RTR-1   OPS-RTR-1#clear ip ospf process
Mon Jan 26 00:21:42 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Mon Jan 26 00:21:49 2026   ENT-ADM-MLS   ENT-ADM-MLS#clear ip ospf process
Mon Jan 26 00:22:33 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 00:22:40 2026   CORE-EDGE   CORE-EDGE#clear ip ospf process
Mon Jan 26 01:06:34 2026   OPS-RTR-1   OPS-RTR-1>ena
Mon Jan 26 01:06:42 2026   OPS-RTR-1   OPS-RTR-1#conf t
Mon Jan 26 01:06:51 2026   OPS-RTR-1   OPS-RTR-1(config)#int g0/0/1
Mon Jan 26 01:07:14 2026   OPS-RTR-1   OPS-RTR-1(config-if)#no ip ospf authentication message-digest
Mon Jan 26 01:07:26 2026   OPS-RTR-1   OPS-RTR-1(config-if)#no ip ospf message-digest-key 1 md5 CISEGCISCO
Mon Jan 26 01:07:49 2026   OPS-RTR-1   OPS-RTR-1(config-if)#int g0/0/0
Mon Jan 26 01:08:17 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf message-digest-key 1 md5 CISEGCISCO
Mon Jan 26 01:08:24 2026   OPS-RTR-1   OPS-RTR-1(config-if)#ip ospf authentication message-digest
Mon Jan 26 01:08:37 2026   OPS-RTR-1   OPS-RTR-1(config-if)#exit
Mon Jan 26 01:08:43 2026   OPS-RTR-1   OPS-RTR-1(config)#exit
Mon Jan 26 01:08:56 2026   OPS-RTR-1   OPS-RTR-1#clear ip ospf process
Mon Jan 26 01:10:57 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Mon Jan 26 12:50:41 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE#conf t 
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#ntp authenticate 
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#ntp trusted-key 10
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#ntp update-calendar
Mon Jan 26 12:51:01 2026   CORE-EDGE   CORE-EDGE(config)#end
Mon Jan 26 12:51:04 2026   CORE-EDGE   CORE-EDGE#copy run start
Mon Jan 26 12:51:34 2026   DMZ-SW   DMZ-SW>ena
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW#conf t 
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#ntp authenticate 
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#ntp trusted-key 10
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#ntp update-calendar
Mon Jan 26 12:51:40 2026   DMZ-SW   DMZ-SW(config)#end
Mon Jan 26 12:51:58 2026   DMZ-SW   DMZ-SW#copy run start
Mon Jan 26 12:57:50 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t 
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ntp authenticate 
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ntp trusted-key 10
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#ntp update-calendar
Mon Jan 26 12:57:55 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#end
Mon Jan 26 12:57:59 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Mon Jan 26 12:58:12 2026   CORE-MLS-1   CORE-MLS-1>ena
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1#conf t 
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp authenticate 
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp trusted-key 10
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp update-calendar
Mon Jan 26 12:58:18 2026   CORE-MLS-1   CORE-MLS-1(config)#end
Mon Jan 26 12:58:20 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Mon Jan 26 12:58:46 2026   OPS-RTR-1   OPS-RTR-1>ena
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1#conf t 
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#ntp authenticate 
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#ntp trusted-key 10
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#ntp update-calendar
Mon Jan 26 12:58:55 2026   OPS-RTR-1   OPS-RTR-1(config)#end
Mon Jan 26 12:58:56 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Mon Jan 26 12:59:13 2026   OPS-RTR-2   OPS-RTR-2>ena
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2#conf t 
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ntp authenticate 
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ntp trusted-key 10
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ntp update-calendar
Mon Jan 26 12:59:19 2026   OPS-RTR-2   OPS-RTR-2(config)#end
Mon Jan 26 12:59:20 2026   OPS-RTR-2   OPS-RTR-2#copy run start
Mon Jan 26 13:00:48 2026   ADM-SW-1   ADM-SW-1>ena
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1#conf t 
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1(config)#ntp authenticate 
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1(config)#ntp trusted-key 10
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:00:53 2026   ADM-SW-1   ADM-SW-1(config)#end
Mon Jan 26 13:00:54 2026   ADM-SW-1   ADM-SW-1#copy run start
Mon Jan 26 13:01:07 2026   ADM-SW-2   ADM-SW-2>ena
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2#conf t 
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2(config)#ntp authenticate 
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2(config)#ntp trusted-key 10
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2(config)#end
Mon Jan 26 13:01:12 2026   ADM-SW-2   ADM-SW-2#copy run start
Mon Jan 26 13:01:32 2026   SOC-SW   SOC-SW>ena
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW#conf t 
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW(config)#ntp authenticate 
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW(config)#ntp trusted-key 10
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:01:37 2026   SOC-SW   SOC-SW(config)#end
Mon Jan 26 13:01:38 2026   SOC-SW   SOC-SW#copy run start
Mon Jan 26 13:01:57 2026   MGMT-SW   MGMT-SW>ena
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW#conf t 
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW(config)#ntp authenticate 
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW(config)#ntp trusted-key 10
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW(config)#end
Mon Jan 26 13:02:02 2026   MGMT-SW   MGMT-SW#copy run start
Mon Jan 26 13:02:16 2026   SERV-FARM-SW   SERV-FARM-SW>ena
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW#conf t 
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ntp authenticate 
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ntp trusted-key 10
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW(config)#end
Mon Jan 26 13:02:22 2026   SERV-FARM-SW   SERV-FARM-SW#copy run start
Mon Jan 26 13:08:58 2026   BRANCH-1   BRANCH-1>ena
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1#conf t 
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#ntp authenticate 
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#ntp authentication-key 20 md5 CISEGCISCO
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#ntp trusted-key 20
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#ntp server 172.24.0.10 key 20
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#ntp update-calendar
Mon Jan 26 13:09:02 2026   BRANCH-1   BRANCH-1(config)#end
Mon Jan 26 13:09:05 2026   BRANCH-1   BRANCH-1#copy run start
Mon Jan 26 13:09:28 2026   SW-BRANCH-1   SW-BRANCH-1>ena
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1#conf t 
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp authenticate 
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp authentication-key 20 md5 CISEGCISCO
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp trusted-key 20
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp server 172.24.0.10 key 20
Mon Jan 26 13:09:34 2026   SW-BRANCH-1   SW-BRANCH-1(config)#end
Mon Jan 26 13:09:36 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Mon Jan 26 13:13:14 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 13:13:20 2026   CORE-EDGE   CORE-EDGE#sh clock
Mon Jan 26 13:13:42 2026   CORE-EDGE   CORE-EDGE#sh ntp status
Mon Jan 26 13:14:09 2026   CORE-EDGE   CORE-EDGE#sh npt associations
Mon Jan 26 13:14:19 2026   CORE-EDGE   CORE-EDGE#sh ntp associations
Mon Jan 26 13:15:35 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:15:47 2026   BRANCH-1   BRANCH-1#sh ntp associations
Mon Jan 26 13:15:56 2026   BRANCH-1   BRANCH-1#sh clock
Mon Jan 26 13:17:55 2026   OPS-RTR-2   OPS-RTR-2>ena
Mon Jan 26 13:18:03 2026   OPS-RTR-2   OPS-RTR-2#sh clock
Mon Jan 26 13:18:09 2026   OPS-RTR-2   OPS-RTR-2#sh ntp status
Mon Jan 26 13:18:29 2026   CORE-EDGE   CORE-EDGE#sh clock
Mon Jan 26 13:18:36 2026   CORE-EDGE   CORE-EDGE#sh ntp associations
Mon Jan 26 13:19:10 2026   CORE-EDGE   CORE-EDGE#sh ntp status
Mon Jan 26 13:21:56 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 13:22:04 2026   CORE-EDGE   CORE-EDGE#sh ntp status
Mon Jan 26 13:22:08 2026   CORE-EDGE   CORE-EDGE#conf t
Mon Jan 26 13:22:44 2026   CORE-EDGE   CORE-EDGE(config)#ntp authenticate
Mon Jan 26 13:23:03 2026   DMZ-SW   DMZ-SW>ena
Mon Jan 26 13:23:12 2026   DMZ-SW   DMZ-SW#sh ntp status
Mon Jan 26 13:23:16 2026   DMZ-SW   DMZ-SW#conf t
Mon Jan 26 13:23:19 2026   DMZ-SW   DMZ-SW(config)#ntp authenticate
Mon Jan 26 13:23:45 2026   CORE-MLS-1   CORE-MLS-1>ena
Mon Jan 26 13:23:53 2026   CORE-MLS-1   CORE-MLS-1#sh clock
Mon Jan 26 13:23:59 2026   CORE-MLS-1   CORE-MLS-1#sh ntp status
Mon Jan 26 13:24:06 2026   CORE-MLS-1   CORE-MLS-1#conf t
Mon Jan 26 13:24:09 2026   CORE-MLS-1   CORE-MLS-1(config)#ntp authenticate
Mon Jan 26 13:24:49 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Mon Jan 26 13:24:57 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ntp status
Mon Jan 26 13:25:12 2026   ENT-ADM-MLS   ENT-ADM-MLS#sh ntp associations
Mon Jan 26 13:25:37 2026   CORE-EDGE   CORE-EDGE(config)#exit
Mon Jan 26 13:25:45 2026   CORE-EDGE   CORE-EDGE#sh ntp status
Mon Jan 26 13:26:02 2026   CORE-EDGE   CORE-EDGE#copy run start
Mon Jan 26 13:26:16 2026   DMZ-SW   DMZ-SW(config)#exit
Mon Jan 26 13:26:22 2026   DMZ-SW   DMZ-SW#sh ntp status
Mon Jan 26 13:26:43 2026   DMZ-SW   DMZ-SW#copy run start
Mon Jan 26 13:26:56 2026   CORE-MLS-1   CORE-MLS-1(config)#end
Mon Jan 26 13:27:06 2026   CORE-MLS-1   CORE-MLS-1#sh ntp status
Mon Jan 26 13:27:13 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Mon Jan 26 13:27:31 2026   DMZ-SW   DMZ-SW#sh ntp status
Mon Jan 26 13:28:28 2026   DMZ-SW   DMZ-SW#conf t
Mon Jan 26 13:28:39 2026   DMZ-SW   DMZ-SW(config)#ntp authenticate
Mon Jan 26 13:28:59 2026   DMZ-SW   DMZ-SW(config)#ntp authentication-key 10 md5 CISEGCISCO
Mon Jan 26 13:29:09 2026   DMZ-SW   DMZ-SW(config)#ntp trusted-key 10
Mon Jan 26 13:29:26 2026   DMZ-SW   DMZ-SW(config)#ntp server 172.16.0.10 key 10
Mon Jan 26 13:29:27 2026   DMZ-SW   DMZ-SW(config)#end
Mon Jan 26 13:29:48 2026   DMZ-SW   DMZ-SW#copy run start
Mon Jan 26 13:30:10 2026   OPS-RTR-1   OPS-RTR-1>ena
Mon Jan 26 13:30:17 2026   OPS-RTR-1   OPS-RTR-1#sh clock
Mon Jan 26 13:30:26 2026   OPS-RTR-1   OPS-RTR-1#sh ntp status
Mon Jan 26 13:30:50 2026   OPS-RTR-2   OPS-RTR-2>ena
Mon Jan 26 13:30:56 2026   OPS-RTR-2   OPS-RTR-2#sh clock
Mon Jan 26 13:31:01 2026   OPS-RTR-2   OPS-RTR-2#sh ntp status
Mon Jan 26 13:31:22 2026   BRANCH-1   BRANCH-1>ena
Mon Jan 26 13:31:26 2026   BRANCH-1   BRANCH-1#sh clock
Mon Jan 26 13:31:31 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:31:57 2026   BRANCH-1   BRANCH-1#conf t
Mon Jan 26 13:33:10 2026   BRANCH-1   BRANCH-1(config)#ntp authenticate
Mon Jan 26 13:33:26 2026   BRANCH-1   BRANCH-1(config)#ntp authentication-key 20 md5 CISEGCISCO
Mon Jan 26 13:33:34 2026   BRANCH-1   BRANCH-1(config)#ntp trusted-key 20
Mon Jan 26 13:33:51 2026   BRANCH-1   BRANCH-1(config)#ntp server 172.24.0.10 key 20
Mon Jan 26 13:34:00 2026   BRANCH-1   BRANCH-1(config)#ntp update-calendar
Mon Jan 26 13:34:01 2026   BRANCH-1   BRANCH-1(config)#end
Mon Jan 26 13:34:07 2026   BRANCH-1   BRANCH-1#copy run start
Mon Jan 26 13:34:19 2026   SW-BRANCH-1   SW-BRANCH-1>ena
Mon Jan 26 13:34:25 2026   SW-BRANCH-1   SW-BRANCH-1#sh clock
Mon Jan 26 13:34:36 2026   SW-BRANCH-1   SW-BRANCH-1#conf t
Mon Jan 26 13:34:47 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp authenticate
Mon Jan 26 13:35:02 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp authentication-key 20 md5 CISEGCISCO
Mon Jan 26 13:35:11 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp trusted-key 20
Mon Jan 26 13:35:22 2026   SW-BRANCH-1   SW-BRANCH-1(config)#ntp server 172.24.0.10 key 20
Mon Jan 26 13:35:24 2026   SW-BRANCH-1   SW-BRANCH-1(config)#end
Mon Jan 26 13:35:28 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Mon Jan 26 13:37:32 2026   DMZ-SW   DMZ-SW#sh clock
Mon Jan 26 13:37:38 2026   DMZ-SW   DMZ-SW#sh ntp status
Mon Jan 26 13:37:51 2026   BRANCH-1   BRANCH-1#sh clock
Mon Jan 26 13:37:55 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:38:21 2026   SW-BRANCH-1   SW-BRANCH-1#sh clock
Mon Jan 26 13:38:26 2026   SW-BRANCH-1   SW-BRANCH-1#sh ntp status
Mon Jan 26 13:38:48 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:40:05 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:40:21 2026   BRANCH-1   BRANCH-1#clear ntp associations
Mon Jan 26 13:40:43 2026   BRANCH-1   BRANCH-1#conf t
Mon Jan 26 13:40:52 2026   BRANCH-1   BRANCH-1(config)#clear ntp associations
Mon Jan 26 13:40:58 2026   BRANCH-1   BRANCH-1(config)#exit
Mon Jan 26 13:41:02 2026   BRANCH-1   BRANCH-1#clear ?
Mon Jan 26 13:41:26 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:41:46 2026   BRANCH-1   BRANCH-1#conf t
Mon Jan 26 13:41:52 2026   BRANCH-1   BRANCH-1(config)#clear ?
Mon Jan 26 13:41:59 2026   BRANCH-1   BRANCH-1(config)#exit
Mon Jan 26 13:43:32 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 13:48:30 2026   BRANCH-1   BRANCH-1#sh ntp status
Mon Jan 26 16:36:47 2026   SW-BRANCH-1   SW-BRANCH-1>ena
Mon Jan 26 16:37:01 2026   SW-BRANCH-1   SW-BRANCH-1#conf t
Mon Jan 26 16:37:01 2026   SW-BRANCH-1   SW-BRANCH-1(config)#service timestamps log datetime msec
Mon Jan 26 16:37:01 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging host 172.16.0.10
Mon Jan 26 16:37:01 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging trap debugging
Mon Jan 26 16:37:05 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging on
Mon Jan 26 16:37:18 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging facility local7
Mon Jan 26 16:37:25 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging ?
Mon Jan 26 16:38:57 2026   SW-BRANCH-1   SW-BRANCH-1(config)#end
Mon Jan 26 16:39:10 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Mon Jan 26 16:44:37 2026   BRANCH-1   BRANCH-1>ena
Mon Jan 26 16:44:43 2026   BRANCH-1   BRANCH-1#conf t
Mon Jan 26 16:44:43 2026   BRANCH-1   BRANCH-1(config)#service timestamps log datetime msec
Mon Jan 26 16:44:43 2026   BRANCH-1   BRANCH-1(config)#logging host 172.16.0.10
Mon Jan 26 16:44:43 2026   BRANCH-1   BRANCH-1(config)#logging trap debugging
Mon Jan 26 16:44:47 2026   BRANCH-1   BRANCH-1(config)#logging on
Mon Jan 26 16:44:57 2026   BRANCH-1   BRANCH-1(config)#end
Mon Jan 26 16:45:02 2026   BRANCH-1   BRANCH-1#copy run start
Mon Jan 26 16:45:27 2026   CORE-EDGE   CORE-EDGE>ena
Mon Jan 26 16:45:37 2026   CORE-EDGE   CORE-EDGE#conf t
Mon Jan 26 16:45:37 2026   CORE-EDGE   CORE-EDGE(config)#service timestamps log datetime msec
Mon Jan 26 16:45:37 2026   CORE-EDGE   CORE-EDGE(config)#logging host 172.16.0.10
Mon Jan 26 16:45:37 2026   CORE-EDGE   CORE-EDGE(config)#logging trap debugging
Mon Jan 26 16:45:39 2026   CORE-EDGE   CORE-EDGE(config)#logging on
Mon Jan 26 16:45:41 2026   CORE-EDGE   CORE-EDGE(config)#end
Mon Jan 26 16:45:46 2026   CORE-EDGE   CORE-EDGE#copy run start
Mon Jan 26 16:46:00 2026   DMZ-SW   DMZ-SW>ena
Mon Jan 26 16:46:05 2026   DMZ-SW   DMZ-SW#conf t
Mon Jan 26 16:46:05 2026   DMZ-SW   DMZ-SW(config)#service timestamps log datetime msec
Mon Jan 26 16:46:05 2026   DMZ-SW   DMZ-SW(config)#logging host 172.16.0.10
Mon Jan 26 16:46:05 2026   DMZ-SW   DMZ-SW(config)#logging trap debugging
Mon Jan 26 16:46:06 2026   DMZ-SW   DMZ-SW(config)#logging on
Mon Jan 26 16:46:07 2026   DMZ-SW   DMZ-SW(config)#end
Mon Jan 26 16:46:13 2026   DMZ-SW   DMZ-SW#copy run start
Mon Jan 26 16:46:32 2026   CORE-MLS-1   CORE-MLS-1>ena
Mon Jan 26 16:46:36 2026   CORE-MLS-1   CORE-MLS-1#conf t
Mon Jan 26 16:46:36 2026   CORE-MLS-1   CORE-MLS-1(config)#service timestamps log datetime msec
Mon Jan 26 16:46:36 2026   CORE-MLS-1   CORE-MLS-1(config)#logging host 172.16.0.10
Mon Jan 26 16:46:36 2026   CORE-MLS-1   CORE-MLS-1(config)#logging trap debugging
Mon Jan 26 16:46:37 2026   CORE-MLS-1   CORE-MLS-1(config)#logging on
Mon Jan 26 16:46:39 2026   CORE-MLS-1   CORE-MLS-1(config)#end
Mon Jan 26 16:46:42 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Mon Jan 26 16:46:53 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Mon Jan 26 16:46:59 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Mon Jan 26 16:46:59 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#service timestamps log datetime msec
Mon Jan 26 16:46:59 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#logging host 172.16.0.10
Mon Jan 26 16:46:59 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#logging trap debugging
Mon Jan 26 16:47:00 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#logging on
Mon Jan 26 16:47:02 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#end
Mon Jan 26 16:47:10 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Mon Jan 26 16:47:22 2026   ADM-SW-1   ADM-SW-1>ena
Mon Jan 26 16:47:28 2026   ADM-SW-1   ADM-SW-1#conf t
Mon Jan 26 16:47:28 2026   ADM-SW-1   ADM-SW-1(config)#service timestamps log datetime msec
Mon Jan 26 16:47:28 2026   ADM-SW-1   ADM-SW-1(config)#logging host 172.16.0.10
Mon Jan 26 16:47:28 2026   ADM-SW-1   ADM-SW-1(config)#logging trap debugging
Mon Jan 26 16:47:29 2026   ADM-SW-1   ADM-SW-1(config)#logging on
Mon Jan 26 16:47:32 2026   ADM-SW-1   ADM-SW-1(config)#end
Mon Jan 26 16:47:36 2026   ADM-SW-1   ADM-SW-1#copy run start
Mon Jan 26 16:47:47 2026   ADM-SW-2   ADM-SW-2>ena
Mon Jan 26 16:47:52 2026   ADM-SW-2   ADM-SW-2#conf t
Mon Jan 26 16:47:52 2026   ADM-SW-2   ADM-SW-2(config)#service timestamps log datetime msec
Mon Jan 26 16:47:52 2026   ADM-SW-2   ADM-SW-2(config)#logging host 172.16.0.10
Mon Jan 26 16:47:52 2026   ADM-SW-2   ADM-SW-2(config)#logging trap debugging
Mon Jan 26 16:47:53 2026   ADM-SW-2   ADM-SW-2(config)#logging on
Mon Jan 26 16:47:54 2026   ADM-SW-2   ADM-SW-2(config)#end
Mon Jan 26 16:48:01 2026   ADM-SW-2   ADM-SW-2#copy run start
Mon Jan 26 16:48:46 2026   OPS-RTR-1   OPS-RTR-1>ena
Mon Jan 26 16:49:03 2026   OPS-RTR-1   OPS-RTR-1#conf t
Mon Jan 26 16:49:03 2026   OPS-RTR-1   OPS-RTR-1(config)#service timestamps log datetime msec
Mon Jan 26 16:49:03 2026   OPS-RTR-1   OPS-RTR-1(config)#logging host 172.16.0.10
Mon Jan 26 16:49:03 2026   OPS-RTR-1   OPS-RTR-1(config)#logging trap debugging
Mon Jan 26 16:49:04 2026   OPS-RTR-1   OPS-RTR-1(config)#logging on
Mon Jan 26 16:49:05 2026   OPS-RTR-1   OPS-RTR-1(config)#end
Mon Jan 26 16:49:10 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Mon Jan 26 16:49:24 2026   SOC-SW   SOC-SW>ena
Mon Jan 26 16:49:28 2026   SOC-SW   SOC-SW#conf t
Mon Jan 26 16:49:28 2026   SOC-SW   SOC-SW(config)#service timestamps log datetime msec
Mon Jan 26 16:49:28 2026   SOC-SW   SOC-SW(config)#logging host 172.16.0.10
Mon Jan 26 16:49:28 2026   SOC-SW   SOC-SW(config)#logging trap debugging
Mon Jan 26 16:49:29 2026   SOC-SW   SOC-SW(config)#logging on
Mon Jan 26 16:49:30 2026   SOC-SW   SOC-SW(config)#end
Mon Jan 26 16:49:37 2026   SOC-SW   SOC-SW#copy run start
Mon Jan 26 16:49:49 2026   OPS-RTR-2   OPS-RTR-2>ena
Mon Jan 26 16:49:53 2026   OPS-RTR-2   OPS-RTR-2#conf t
Mon Jan 26 16:49:53 2026   OPS-RTR-2   OPS-RTR-2(config)#service timestamps log datetime msec
Mon Jan 26 16:49:53 2026   OPS-RTR-2   OPS-RTR-2(config)#logging host 172.16.0.10
Mon Jan 26 16:49:53 2026   OPS-RTR-2   OPS-RTR-2(config)#logging trap debugging
Mon Jan 26 16:49:54 2026   OPS-RTR-2   OPS-RTR-2(config)#logging on
Mon Jan 26 16:49:55 2026   OPS-RTR-2   OPS-RTR-2(config)#end
Mon Jan 26 16:50:01 2026   OPS-RTR-2   OPS-RTR-2#copy run start
Mon Jan 26 16:50:15 2026   SERV-FARM-SW   SERV-FARM-SW>ena
Mon Jan 26 16:50:20 2026   SERV-FARM-SW   SERV-FARM-SW#conf t
Mon Jan 26 16:50:20 2026   SERV-FARM-SW   SERV-FARM-SW(config)#service timestamps log datetime msec
Mon Jan 26 16:50:20 2026   SERV-FARM-SW   SERV-FARM-SW(config)#logging host 172.16.0.10
Mon Jan 26 16:50:20 2026   SERV-FARM-SW   SERV-FARM-SW(config)#logging trap debugging
Mon Jan 26 16:50:21 2026   SERV-FARM-SW   SERV-FARM-SW(config)#logging on
Mon Jan 26 16:50:23 2026   SERV-FARM-SW   SERV-FARM-SW(config)#end
Mon Jan 26 16:50:28 2026   SERV-FARM-SW   SERV-FARM-SW#copy run start
Mon Jan 26 16:50:39 2026   MGMT-SW   MGMT-SW>ena
Mon Jan 26 16:50:44 2026   MGMT-SW   MGMT-SW#conf t
Mon Jan 26 16:50:44 2026   MGMT-SW   MGMT-SW(config)#service timestamps log datetime msec
Mon Jan 26 16:50:44 2026   MGMT-SW   MGMT-SW(config)#logging host 172.16.0.10
Mon Jan 26 16:50:44 2026   MGMT-SW   MGMT-SW(config)#logging trap debugging
Mon Jan 26 16:50:45 2026   MGMT-SW   MGMT-SW(config)#logging on
Mon Jan 26 16:50:46 2026   MGMT-SW   MGMT-SW(config)#end
Mon Jan 26 16:50:53 2026   MGMT-SW   MGMT-SW#copy run start
Mon Jan 26 16:59:33 2026   BRANCH-1   BRANCH-1>ena
Mon Jan 26 16:59:38 2026   BRANCH-1   BRANCH-1#conf t
Mon Jan 26 16:59:38 2026   BRANCH-1   BRANCH-1(config)#service timestamps log datetime msec
Mon Jan 26 16:59:38 2026   BRANCH-1   BRANCH-1(config)#logging host 172.24.0.10
Mon Jan 26 16:59:38 2026   BRANCH-1   BRANCH-1(config)#logging trap debugging
Mon Jan 26 16:59:41 2026   BRANCH-1   BRANCH-1(config)#logging on
Mon Jan 26 16:59:46 2026   BRANCH-1   BRANCH-1(config)#end
Mon Jan 26 16:59:51 2026   BRANCH-1   BRANCH-1#copy run start
Mon Jan 26 17:00:03 2026   SW-BRANCH-1   SW-BRANCH-1>ena
Mon Jan 26 17:00:09 2026   SW-BRANCH-1   SW-BRANCH-1#conf t
Mon Jan 26 17:00:09 2026   SW-BRANCH-1   SW-BRANCH-1(config)#service timestamps log datetime msec
Mon Jan 26 17:00:09 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging host 172.24.0.10
Mon Jan 26 17:00:09 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging trap debugging
Mon Jan 26 17:00:11 2026   SW-BRANCH-1   SW-BRANCH-1(config)#logging on
Mon Jan 26 17:00:15 2026   SW-BRANCH-1   SW-BRANCH-1(config)#end
Mon Jan 26 17:00:20 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Mon Jan 26 17:06:40 2026   BRANCH-1   BRANCH-1#sh logging
Mon Jan 26 17:13:01 2026   BRANCH-1   BRANCH-1#copy run start
Tue Jan 27 22:56:56 2026   CORE-EDGE   CORE-EDGE>ena
Tue Jan 27 22:57:10 2026   CORE-EDGE   CORE-EDGE#conf t
Tue Jan 27 22:57:20 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/0
Tue Jan 27 22:57:31 2026   CORE-EDGE   CORE-EDGE(config-if)#ip nat outside
Tue Jan 27 22:57:39 2026   CORE-EDGE   CORE-EDGE(config-if)#int g0/0/1
Tue Jan 27 22:57:47 2026   CORE-EDGE   CORE-EDGE(config-if)#ip nat inside
Tue Jan 27 22:57:55 2026   CORE-EDGE   CORE-EDGE(config-if)#int g0/0/2
Tue Jan 27 22:58:03 2026   CORE-EDGE   CORE-EDGE(config-if)#ip nat inside
Tue Jan 27 22:58:08 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Tue Jan 27 22:58:17 2026   CORE-EDGE   CORE-EDGE(config)#ip nat inside source static 172.16.1.10 203.0.113.10
Tue Jan 27 22:58:28 2026   CORE-EDGE   CORE-EDGE(config)#ip nat inside source static 172.16.1.11 203.0.113.11
Tue Jan 27 22:58:37 2026   CORE-EDGE   CORE-EDGE(config)#ip nat inside source static 172.16.1.12 203.0.113.12
Tue Jan 27 22:59:01 2026   CORE-EDGE   CORE-EDGE(config)#access-list 110 permit ip 172.16.0.0 0.7.255.255 any
Tue Jan 27 22:59:17 2026   CORE-EDGE   CORE-EDGE(config)#ip nat pool PAT-CORPORATE 203.0.113.128 203.0.113.130 netmask 255.255.255.224
Tue Jan 27 22:59:28 2026   CORE-EDGE   CORE-EDGE(config)#ip nat inside source list 110 pool PAT-CORPORATE overload
Tue Jan 27 22:59:37 2026   CORE-EDGE   CORE-EDGE(config)#ip access-list extended 110
Tue Jan 27 22:59:45 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#1 deny ip 172.16.0.0 0.7.255.255 172.24.0.0 0.7.255.255
Tue Jan 27 22:59:48 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#end
Tue Jan 27 23:00:48 2026   BRANCH-1   BRANCH-1>ena
Tue Jan 27 23:00:53 2026   BRANCH-1   BRANCH-1#conf t
Tue Jan 27 23:01:06 2026   BRANCH-1   BRANCH-1(config)#ip route 0.0.0.0 0.0.0.0 198.51.100.254
Tue Jan 27 23:01:12 2026   BRANCH-1   BRANCH-1(config)#int g0/0/2
Tue Jan 27 23:01:20 2026   BRANCH-1   BRANCH-1(config-if)#ip nat outside
Tue Jan 27 23:01:25 2026   BRANCH-1   BRANCH-1(config-if)#int g0/0/0
Tue Jan 27 23:01:32 2026   BRANCH-1   BRANCH-1(config-if)#ip nat inside
Tue Jan 27 23:01:41 2026   BRANCH-1   BRANCH-1(config-if)#access-list 111 permit ip 172.24.0.0 0.7.255.255 any
Tue Jan 27 23:02:12 2026   BRANCH-1   BRANCH-1(config)#ip nat pool PAT-BRANCH 198.51.100.128 198.51.100.130 netmask 255.255.255.224
Tue Jan 27 23:02:25 2026   BRANCH-1   BRANCH-1(config)#ip nat inside source list 111 pool PAT-BRANCH overload
Tue Jan 27 23:02:32 2026   BRANCH-1   BRANCH-1(config)#ip access-list extended 111
Tue Jan 27 23:02:41 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#1 deny ip 172.24.0.0 0.7.255.255 172.16.0.0 0.7.255.255
Tue Jan 27 23:02:49 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#end
Tue Jan 27 23:03:04 2026   CORE-EDGE   CORE-EDGE#conf t
Tue Jan 27 23:03:19 2026   CORE-EDGE   CORE-EDGE(config)#crypto isakmp policy 1
Tue Jan 27 23:03:26 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#hash sha
Tue Jan 27 23:03:32 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#authentication pre-share
Tue Jan 27 23:03:38 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#group 5
Tue Jan 27 23:03:42 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#lifetime 3600
Tue Jan 27 23:03:48 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#encryption aes 256
Tue Jan 27 23:03:52 2026   CORE-EDGE   CORE-EDGE(config-isakmp)#exit
Tue Jan 27 23:03:59 2026   CORE-EDGE   CORE-EDGE(config)#crypto isakmp key CISEGCISCO address 198.51.100.1
Tue Jan 27 23:04:09 2026   CORE-EDGE   CORE-EDGE(config)#access-list 101 permit ip 172.16.0.0 0.7.255.255 172.24.0.0 0.7.255.255
Tue Jan 27 23:04:23 2026   CORE-EDGE   CORE-EDGE(config)#crypto ipsec transform-set COREEDGE-BRANCH esp-aes esp-sha-hmac
Tue Jan 27 23:04:31 2026   CORE-EDGE   CORE-EDGE(config)#crypto map MAP-COREEDGE-BRANCH 10 ipsec-isakmp
Tue Jan 27 23:04:53 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#match address 101
Tue Jan 27 23:05:02 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#set transform-set COREEDGE-BRANCH
Tue Jan 27 23:05:09 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#set peer 198.51.100.1
Tue Jan 27 23:05:15 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#set pfs group5
Tue Jan 27 23:05:22 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#set security-association lifetime seconds 900
Tue Jan 27 23:05:28 2026   CORE-EDGE   CORE-EDGE(config-crypto-map)#exit
Tue Jan 27 23:05:34 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/0
Tue Jan 27 23:05:42 2026   CORE-EDGE   CORE-EDGE(config-if)#crypto map MAP-COREEDGE-BRANCH
Tue Jan 27 23:05:48 2026   CORE-EDGE   CORE-EDGE(config-if)#end
Tue Jan 27 23:06:00 2026   CORE-EDGE   CORE-EDGE#copy run start
Tue Jan 27 23:06:11 2026   BRANCH-1   BRANCH-1#conf t
Tue Jan 27 23:06:19 2026   BRANCH-1   BRANCH-1(config)#crypto isakmp policy 1
Tue Jan 27 23:06:27 2026   BRANCH-1   BRANCH-1(config-isakmp)#hash sha
Tue Jan 27 23:06:33 2026   BRANCH-1   BRANCH-1(config-isakmp)#authentication pre-share
Tue Jan 27 23:06:40 2026   BRANCH-1   BRANCH-1(config-isakmp)#group 5
Tue Jan 27 23:06:49 2026   BRANCH-1   BRANCH-1(config-isakmp)#lifetime 3600
Tue Jan 27 23:07:01 2026   BRANCH-1   BRANCH-1(config-isakmp)#encryption aes 256
Tue Jan 27 23:07:04 2026   BRANCH-1   BRANCH-1(config-isakmp)#exit
Tue Jan 27 23:07:12 2026   BRANCH-1   BRANCH-1(config)#crypto isakmp key CISEGCISCO address 203.0.113.1
Tue Jan 27 23:07:23 2026   BRANCH-1   BRANCH-1(config)#access-list 102 permit ip 172.24.0.0 0.7.255.255 172.16.0.0 0.7.255.255
Tue Jan 27 23:07:36 2026   BRANCH-1   BRANCH-1(config)#crypto ipsec transform-set BRANCH-COREEDGE esp-aes esp-sha-hmac
Tue Jan 27 23:07:51 2026   BRANCH-1   BRANCH-1(config)#crypto map MAP-BRANCH-COREEDGE 10 ipsec-isakmp
Tue Jan 27 23:07:59 2026   BRANCH-1   BRANCH-1(config-crypto-map)#set peer 203.0.113.1
Tue Jan 27 23:08:12 2026   BRANCH-1   BRANCH-1(config-crypto-map)#set pfs group5
Tue Jan 27 23:08:20 2026   BRANCH-1   BRANCH-1(config-crypto-map)#set transform-set BRANCH-COREEDGE
Tue Jan 27 23:08:27 2026   BRANCH-1   BRANCH-1(config-crypto-map)#match address 102
Tue Jan 27 23:08:33 2026   BRANCH-1   BRANCH-1(config-crypto-map)#set security-association lifetime seconds 900
Tue Jan 27 23:08:35 2026   BRANCH-1   BRANCH-1(config-crypto-map)#exit
Tue Jan 27 23:08:51 2026   BRANCH-1   BRANCH-1(config)#int g0/0/2
Tue Jan 27 23:08:57 2026   BRANCH-1   BRANCH-1(config-if)#crypto map MAP-BRANCH-COREEDGE
Tue Jan 27 23:09:02 2026   BRANCH-1   BRANCH-1(config-if)#end
Tue Jan 27 23:09:09 2026   BRANCH-1   BRANCH-1#copy run start
Tue Jan 27 23:09:43 2026   BRANCH-1   BRANCH-1#sh isakmp ipsec sa
Tue Jan 27 23:10:11 2026   BRANCH-1   BRANCH-1#sh crypto isakmp sa
Tue Jan 27 23:11:00 2026   BRANCH-1   BRANCH-1#sh crypto ipsec sa
Tue Jan 27 23:11:33 2026   BRANCH-1   BRANCH-1#ping 172.16.1.10
Tue Jan 27 23:11:51 2026   BRANCH-1   BRANCH-1#ping 172.16.1.10
Tue Jan 27 23:18:15 2026   ISP   ISP>ena
Tue Jan 27 23:18:29 2026   ISP   ISP#ping 203.0.113.10
Tue Jan 27 23:18:41 2026   ISP   ISP#ping 203.0.113.11
Tue Jan 27 23:18:54 2026   ISP   ISP#ping 203.0.113.12
Tue Jan 27 23:19:04 2026   ISP   ISP#ping 172.16.1.10
Wed Jan 28 00:31:19 2026   CORE-EDGE   CORE-EDGE>ena
Wed Jan 28 00:31:25 2026   CORE-EDGE   CORE-EDGE#conf t
Wed Jan 28 00:31:32 2026   CORE-EDGE   CORE-EDGE(config)#ip access-list extended 110
Wed Jan 28 00:32:20 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#11 permit ip 172.16.0.0 0.7.255.255 any
Wed Jan 28 00:32:35 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#exit
Wed Jan 28 00:33:19 2026   CORE-EDGE   CORE-EDGE(config)#end
Wed Jan 28 00:33:23 2026   CORE-EDGE   CORE-EDGE#copy run start
Wed Jan 28 00:34:01 2026   BRANCH-1   BRANCH-1>ena
Wed Jan 28 00:34:06 2026   BRANCH-1   BRANCH-1#conf t
Wed Jan 28 00:34:10 2026   BRANCH-1   BRANCH-1(config)#ip access-list extended 111
Wed Jan 28 00:34:40 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#11 permit ip 172.24.0.0 0.7.255.255 any
Wed Jan 28 00:34:42 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#exit
Wed Jan 28 00:34:56 2026   BRANCH-1   BRANCH-1(config)#exit
Wed Jan 28 00:35:07 2026   BRANCH-1   BRANCH-1#clear ip nat translation
Wed Jan 28 00:35:18 2026   BRANCH-1   BRANCH-1#clear ip nat translation ?
Wed Jan 28 00:35:34 2026   BRANCH-1   BRANCH-1#copy run start
Wed Jan 28 00:36:59 2026   CORE-EDGE   CORE-EDGE#conf t
Wed Jan 28 00:37:26 2026   CORE-EDGE   CORE-EDGE(config)#ip nat inside source list 110 pool PAT-CORPORATE overload
Wed Jan 28 00:37:44 2026   CORE-EDGE   CORE-EDGE(config)#int g0/0/0
Wed Jan 28 00:37:46 2026   CORE-EDGE   CORE-EDGE(config-if)#shut
Wed Jan 28 00:37:50 2026   CORE-EDGE   CORE-EDGE(config-if)#no shut
Wed Jan 28 00:37:59 2026   CORE-EDGE   CORE-EDGE(config-if)#int g0/0/2
Wed Jan 28 00:38:01 2026   CORE-EDGE   CORE-EDGE(config-if)#shut
Wed Jan 28 00:38:04 2026   CORE-EDGE   CORE-EDGE(config-if)#no shut
Wed Jan 28 00:38:21 2026   CORE-EDGE   CORE-EDGE(config-if)#end
Wed Jan 28 00:38:36 2026   CORE-EDGE   CORE-EDGE#clear ip nat translation *
Wed Jan 28 00:38:58 2026   CORE-EDGE   CORE-EDGE#copy run start
Wed Jan 28 00:39:45 2026   BRANCH-1   BRANCH-1#conf t
Wed Jan 28 00:39:48 2026   BRANCH-1   BRANCH-1(config)#ip nat inside source list 111 pool PAT-BRANCH overload
Wed Jan 28 00:40:40 2026   BRANCH-1   BRANCH-1(config)#int g0/0/0
Wed Jan 28 00:40:41 2026   BRANCH-1   BRANCH-1(config-if)#shut
Wed Jan 28 00:40:46 2026   BRANCH-1   BRANCH-1(config-if)#no shut
Wed Jan 28 00:41:00 2026   BRANCH-1   BRANCH-1(config-if)#int g0/0/2
Wed Jan 28 00:41:02 2026   BRANCH-1   BRANCH-1(config-if)#shut
Wed Jan 28 00:41:05 2026   BRANCH-1   BRANCH-1(config-if)#no shut
Wed Jan 28 00:41:21 2026   BRANCH-1   BRANCH-1(config-if)#end
Wed Jan 28 00:41:24 2026   BRANCH-1   BRANCH-1#clear ip nat translation *
Wed Jan 28 00:41:29 2026   BRANCH-1   BRANCH-1#copy run start
Thu Jan 29 21:16:57 2026   SERV-FARM-SW   SERV-FARM-SW>ena
Thu Jan 29 21:18:00 2026   SERV-FARM-SW   SERV-FARM-SW#acc 1 permit host 172.16.1.140
Thu Jan 29 21:18:17 2026   SERV-FARM-SW   SERV-FARM-SW#conf t
Thu Jan 29 21:18:29 2026   SERV-FARM-SW   SERV-FARM-SW(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:18:36 2026   SERV-FARM-SW   SERV-FARM-SW(config)#line vty 0 15
Thu Jan 29 21:18:44 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#access-class 1 in
Thu Jan 29 21:18:46 2026   SERV-FARM-SW   SERV-FARM-SW(config-line)#exit
Thu Jan 29 21:20:16 2026   SERV-FARM-SW   SERV-FARM-SW(config)#end
Thu Jan 29 21:20:20 2026   SERV-FARM-SW   SERV-FARM-SW#copy run start
Thu Jan 29 21:21:00 2026   MGMT-SW   MGMT-SW>ena
Thu Jan 29 21:21:07 2026   MGMT-SW   MGMT-SW#conf t
Thu Jan 29 21:21:07 2026   MGMT-SW   MGMT-SW(config)#acc 1 permit host 10.140.0.50
Thu Jan 29 21:21:07 2026   MGMT-SW   MGMT-SW(config)#line vty 0 15
Thu Jan 29 21:21:07 2026   MGMT-SW   MGMT-SW(config-line)#access-class 1 in
Thu Jan 29 21:21:22 2026   MGMT-SW   MGMT-SW(config-line)#end
Thu Jan 29 21:21:28 2026   MGMT-SW   MGMT-SW#copy run start
Thu Jan 29 21:22:50 2026   MGMT-SW   MGMT-SW#conf t
Thu Jan 29 21:23:02 2026   MGMT-SW   MGMT-SW(config)#no acc 1 permit host 10.140.0.50
Thu Jan 29 21:23:28 2026   MGMT-SW   MGMT-SW(config)#end
Thu Jan 29 21:23:31 2026   MGMT-SW   MGMT-SW#conf t
Thu Jan 29 21:23:47 2026   MGMT-SW   MGMT-SW(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:23:56 2026   MGMT-SW   MGMT-SW(config)#line vty 0 15
Thu Jan 29 21:24:03 2026   MGMT-SW   MGMT-SW(config-line)#access-class 1 in
Thu Jan 29 21:24:05 2026   MGMT-SW   MGMT-SW(config-line)#end
Thu Jan 29 21:24:09 2026   MGMT-SW   MGMT-SW#copy run start
Thu Jan 29 21:24:40 2026   SOC-SW   SOC-SW>ena
Thu Jan 29 21:24:55 2026   SOC-SW   SOC-SW#conf t
Thu Jan 29 21:24:55 2026   SOC-SW   SOC-SW(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:24:55 2026   SOC-SW   SOC-SW(config)#line vty 0 15
Thu Jan 29 21:24:55 2026   SOC-SW   SOC-SW(config-line)#access-class 1 in
Thu Jan 29 21:25:00 2026   SOC-SW   SOC-SW(config-line)#end
Thu Jan 29 21:25:05 2026   SOC-SW   SOC-SW#copy run start
Thu Jan 29 21:26:02 2026   DMZ-SW   DMZ-SW>ena
Thu Jan 29 21:26:09 2026   DMZ-SW   DMZ-SW#conf t
Thu Jan 29 21:26:09 2026   DMZ-SW   DMZ-SW(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:26:09 2026   DMZ-SW   DMZ-SW(config)#line vty 0 15
Thu Jan 29 21:26:09 2026   DMZ-SW   DMZ-SW(config-line)#access-class 1 in
Thu Jan 29 21:26:11 2026   DMZ-SW   DMZ-SW(config-line)#end
Thu Jan 29 21:26:16 2026   DMZ-SW   DMZ-SW#copy run start
Thu Jan 29 21:26:54 2026   SW-BRANCH-1   SW-BRANCH-1>ena
Thu Jan 29 21:26:59 2026   SW-BRANCH-1   SW-BRANCH-1#conf t
Thu Jan 29 21:26:59 2026   SW-BRANCH-1   SW-BRANCH-1(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:26:59 2026   SW-BRANCH-1   SW-BRANCH-1(config)#line vty 0 15
Thu Jan 29 21:26:59 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#access-class 1 in
Thu Jan 29 21:27:02 2026   SW-BRANCH-1   SW-BRANCH-1(config-line)#end
Thu Jan 29 21:27:06 2026   SW-BRANCH-1   SW-BRANCH-1#copy run start
Thu Jan 29 21:27:23 2026   ADM-SW-1   ADM-SW-1>ena
Thu Jan 29 21:27:30 2026   ADM-SW-1   ADM-SW-1#conf t
Thu Jan 29 21:27:30 2026   ADM-SW-1   ADM-SW-1(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:27:30 2026   ADM-SW-1   ADM-SW-1(config)#line vty 0 15
Thu Jan 29 21:27:30 2026   ADM-SW-1   ADM-SW-1(config-line)#access-class 1 in
Thu Jan 29 21:27:33 2026   ADM-SW-1   ADM-SW-1(config-line)#end
Thu Jan 29 21:27:39 2026   ADM-SW-1   ADM-SW-1#copy run start
Thu Jan 29 21:28:02 2026   ADM-SW-2   ADM-SW-2>ena
Thu Jan 29 21:28:07 2026   ADM-SW-2   ADM-SW-2#conf t
Thu Jan 29 21:28:07 2026   ADM-SW-2   ADM-SW-2(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:28:07 2026   ADM-SW-2   ADM-SW-2(config)#line vty 0 15
Thu Jan 29 21:28:07 2026   ADM-SW-2   ADM-SW-2(config-line)#access-class 1 in
Thu Jan 29 21:28:09 2026   ADM-SW-2   ADM-SW-2(config-line)#end
Thu Jan 29 21:28:13 2026   ADM-SW-2   ADM-SW-2#copy run start
Thu Jan 29 21:28:54 2026   ENT-ADM-MLS   ENT-ADM-MLS>ena
Thu Jan 29 21:29:03 2026   ENT-ADM-MLS   ENT-ADM-MLS#conf t
Thu Jan 29 21:29:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:29:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(config)#line vty 0 15
Thu Jan 29 21:29:03 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#access-class 1 in
Thu Jan 29 21:29:13 2026   ENT-ADM-MLS   ENT-ADM-MLS(config-line)#end
Thu Jan 29 21:29:18 2026   ENT-ADM-MLS   ENT-ADM-MLS#copy run start
Thu Jan 29 21:30:39 2026   CORE-MLS-1   CORE-MLS-1>ena
Thu Jan 29 21:30:45 2026   CORE-MLS-1   CORE-MLS-1#conf t
Thu Jan 29 21:30:45 2026   CORE-MLS-1   CORE-MLS-1(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:30:45 2026   CORE-MLS-1   CORE-MLS-1(config)#line vty 0 15
Thu Jan 29 21:30:45 2026   CORE-MLS-1   CORE-MLS-1(config-line)#access-class 1 in
Thu Jan 29 21:30:50 2026   CORE-MLS-1   CORE-MLS-1(config-line)#end
Thu Jan 29 21:34:32 2026   CORE-MLS-1   CORE-MLS-1#copy run start
Thu Jan 29 21:35:04 2026   OPS-RTR-2   OPS-RTR-2>ena
Thu Jan 29 21:35:11 2026   OPS-RTR-2   OPS-RTR-2#conf t
Thu Jan 29 21:35:11 2026   OPS-RTR-2   OPS-RTR-2(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:35:11 2026   OPS-RTR-2   OPS-RTR-2(config)#line vty 0 15
Thu Jan 29 21:35:11 2026   OPS-RTR-2   OPS-RTR-2(config-line)#access-class 1 in
Thu Jan 29 21:35:14 2026   OPS-RTR-2   OPS-RTR-2(config-line)#end
Thu Jan 29 21:35:19 2026   OPS-RTR-2   OPS-RTR-2#copy run start
Thu Jan 29 21:35:56 2026   OPS-RTR-1   OPS-RTR-1>ena
Thu Jan 29 21:36:05 2026   OPS-RTR-1   OPS-RTR-1#conf t
Thu Jan 29 21:36:05 2026   OPS-RTR-1   OPS-RTR-1(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:36:05 2026   OPS-RTR-1   OPS-RTR-1(config)#line vty 0 15
Thu Jan 29 21:36:05 2026   OPS-RTR-1   OPS-RTR-1(config-line)#access-class 1 in
Thu Jan 29 21:36:08 2026   OPS-RTR-1   OPS-RTR-1(config-line)#end
Thu Jan 29 21:36:24 2026   OPS-RTR-1   OPS-RTR-1#copy run start
Thu Jan 29 21:40:15 2026   CORE-EDGE   CORE-EDGE>ena
Thu Jan 29 21:40:20 2026   CORE-EDGE   CORE-EDGE#conf t
Thu Jan 29 21:40:20 2026   CORE-EDGE   CORE-EDGE(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:40:20 2026   CORE-EDGE   CORE-EDGE(config)#line vty 0 15
Thu Jan 29 21:40:20 2026   CORE-EDGE   CORE-EDGE(config-line)#access-class 1 in
Thu Jan 29 21:40:23 2026   CORE-EDGE   CORE-EDGE(config-line)#end
Thu Jan 29 21:40:28 2026   CORE-EDGE   CORE-EDGE#copy run start
Thu Jan 29 21:40:43 2026   BRANCH-1   BRANCH-1>ena
Thu Jan 29 21:40:48 2026   BRANCH-1   BRANCH-1#conf t
Thu Jan 29 21:40:48 2026   BRANCH-1   BRANCH-1(config)#acc 1 permit host 172.16.1.140
Thu Jan 29 21:40:48 2026   BRANCH-1   BRANCH-1(config)#line vty 0 15
Thu Jan 29 21:40:48 2026   BRANCH-1   BRANCH-1(config-line)#access-class 1 in
Thu Jan 29 21:40:50 2026   BRANCH-1   BRANCH-1(config-line)#end
Thu Jan 29 21:40:55 2026   BRANCH-1   BRANCH-1#copy run start
Thu Jan 29 21:44:31 2026   CORE-EDGE   CORE-EDGE#conf t
Thu Jan 29 21:44:50 2026   CORE-EDGE   CORE-EDGE(config)#ip access-list extended OUTBOUND-TRAFFIC
Thu Jan 29 21:45:24 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#remark Bloquear servidores internos excepto DMZ e SYSLOG
Thu Jan 29 21:46:06 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#deny ip host 172.16.40.12 any
Thu Jan 29 21:46:34 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#deny ip host 172.16.1.200 any
Thu Jan 29 21:46:42 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#deny ip host 172.16.1.201 any
Thu Jan 29 21:47:13 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#deny ip host 172.16.1.141 any
Thu Jan 29 21:47:18 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#deny ip host 172.16.1.142 any
Thu Jan 29 21:48:22 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#remark Permitir SYSLOG no port TCP 6514
Thu Jan 29 21:49:30 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#permit tcp host 172.16.0.10 any eq 6514
Thu Jan 29 21:50:06 2026   CORE-EDGE   CORE-EDGE(config-ext-nacl)#int g0/0/2
Thu Jan 29 21:50:58 2026   CORE-EDGE   CORE-EDGE(config-if)#ip access-group OUTBOUND-TRAFFIC out
Thu Jan 29 21:52:07 2026   CORE-EDGE   CORE-EDGE(config-if)#exit
Thu Jan 29 21:54:45 2026   BRANCH-1   BRANCH-1>ena
Thu Jan 29 21:54:50 2026   BRANCH-1   BRANCH-1#conf t
Thu Jan 29 21:55:39 2026   BRANCH-1   BRANCH-1(config)#ip -access-list extended OUTBOUND-TRAFFIC-NAS2
Thu Jan 29 21:55:45 2026   BRANCH-1   BRANCH-1(config)#ip access-list extended OUTBOUND-TRAFFIC-NAS2
Thu Jan 29 21:56:24 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#remark Permitir NAS-2 no port tcp 3389
Thu Jan 29 21:57:33 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#permit tcp host 172.24.0.10 any eq 3389
Thu Jan 29 21:57:59 2026   BRANCH-1   BRANCH-1(config-ext-nacl)#int g0/0/2
Thu Jan 29 21:58:22 2026   BRANCH-1   BRANCH-1(config-if)#ip access-group OUTBOUND-TRAFFIC-NAS2 out
Thu Jan 29 21:58:32 2026   BRANCH-1   BRANCH-1(config-if)#exit
Thu Jan 29 21:59:09 2026   BRANCH-1   BRANCH-1(config)#end
Thu Jan 29 21:59:13 2026   BRANCH-1   BRANCH-1#copy run start
Thu Jan 29 22:03:34 2026   CORE-EDGE   CORE-EDGE>ena
Thu Jan 29 22:03:43 2026   CORE-EDGE   CORE-EDGE#copy run start
Thu Jan 29 22:04:02 2026   OPS-RTR-2   OPS-RTR-2>ena
Thu Jan 29 22:04:09 2026   OPS-RTR-2   OPS-RTR-2#conf ty
Thu Jan 29 22:04:12 2026   OPS-RTR-2   OPS-RTR-2#conf t
Thu Jan 29 22:05:37 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC
Thu Jan 29 22:12:36 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.200 range 31000 31002
Thu Jan 29 22:12:54 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.200 range 31000 31002
Thu Jan 29 22:13:09 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.201 range 31000 31002
Thu Jan 29 22:13:19 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.201 range 31000 31002
Thu Jan 29 22:13:49 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#int g0/0/0
Thu Jan 29 22:14:15 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip access-group INSIDE-TRAFFIC out
Thu Jan 29 22:14:21 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Thu Jan 29 22:19:34 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC
Thu Jan 29 22:20:10 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#5 permit ip host 172.16.1.140 any
Thu Jan 29 22:20:12 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#exit
Thu Jan 29 22:21:51 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC-NET
Thu Jan 29 22:22:28 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit ip any host 172.16.1.140
Thu Jan 29 22:22:35 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark LDAP
Thu Jan 29 22:27:27 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 389
Thu Jan 29 22:27:49 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 389
Thu Jan 29 22:28:36 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 389
Thu Jan 29 22:29:06 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#no permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 389
Thu Jan 29 22:29:18 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark LDAPs
Thu Jan 29 22:29:47 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 636
Thu Jan 29 22:29:57 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 636
Thu Jan 29 22:30:26 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark KERBEROS AUTH
Thu Jan 29 22:30:54 2026   OPS-RTR-2   OPS-RTR-2#conf t
Thu Jan 29 22:31:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC-NET
Thu Jan 29 22:31:42 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark KERBEROS AUTH
Thu Jan 29 22:32:06 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 88
Thu Jan 29 22:32:12 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 88
Thu Jan 29 22:32:42 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark SMTP
Thu Jan 29 22:33:18 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 465
Thu Jan 29 22:33:30 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 587
Thu Jan 29 22:33:35 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 465
Thu Jan 29 22:33:40 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 587
Thu Jan 29 22:33:55 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark FTP
Thu Jan 29 22:34:19 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.141 eq 445
Thu Jan 29 22:34:32 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 445
Thu Jan 29 22:34:56 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#remark HTTPS DC02
Thu Jan 29 22:35:46 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit tcp 172.16.0.0 0.15.255.255 host 172.16.1.142 eq 443
Thu Jan 29 22:36:14 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#exit
Thu Jan 29 22:36:54 2026   OPS-RTR-2   OPS-RTR-2(config)#int g0/0/1
Thu Jan 29 22:37:08 2026   OPS-RTR-2   OPS-RTR-2(config-if)#ip access-group INSIDE-TRAFFIC-NET out
Thu Jan 29 22:37:10 2026   OPS-RTR-2   OPS-RTR-2(config-if)#exit
Thu Jan 29 22:37:53 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC-NET
Thu Jan 29 22:38:53 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp host 172.16.1.12 any eq 53
Thu Jan 29 22:38:58 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#exit
Thu Jan 29 22:39:19 2026   OPS-RTR-2   OPS-RTR-2(config)#ip access-list extended INSIDE-TRAFFIC
Thu Jan 29 22:39:47 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#permit udp host 172.16.1.12 any eq domain
Thu Jan 29 22:39:50 2026   OPS-RTR-2   OPS-RTR-2(config-ext-nacl)#exit
Thu Jan 29 22:39:55 2026   OPS-RTR-2   OPS-RTR-2(config)#end
Thu Jan 29 22:40:00 2026   OPS-RTR-2   OPS-RTR-2#copy run start
