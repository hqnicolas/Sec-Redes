# Computer Networks Project Report

  - **Course:** Computer Engineering
  - **Student:** Nicolas Pereira
  - **Professor:** Humberto Antonio Pedroso
  - **Institution:** Centro Universitário - SATC
  - **Location:** Criciúma
  - **Year:** 2025

-----

## Building Layout

The carrier's floor plan is organized into several distinct areas to optimize workflow and functionality.

  - **Warehouses**: Two warehouses are included, one with an area of approximately $448m^{2}$ and another of $1590m^{2}$. These spaces are designated for material and merchandise storage, keeping administrative and circulation areas clear.

  - **Offices**: There are six numbered offices (01 to 06), each providing multiple independent workspaces with their own specific dimensions.

  - **Meeting Rooms**: The plan includes two identified meeting rooms, offering private spaces for meetings, negotiations, or team sessions.

  - **Common Areas**:

      - A pantry area with a space of 7.14 $m^{2}$.
      - An archive room of about 8.32 $m^{2}$ for storing important documents.
      - Corridors, covering approximately 691.37 $m^{2}$, connect all functional areas, facilitating easy movement throughout the building.

  - **Support Areas**: The layout also details additional circulation zones, workspaces, and support spaces that contribute to the building's overall organization and functionality.

-----

## Logical Network Model

The main network is `192.168.72.0/22`, which provides capacity for 1024 IPs. This leaves IPs from `192.168.72.64/26` onwards available for future VLANs or hosts.

| VLAN | Mask | Hosts | Subnet | IP Range | Gateway IP |
| :--- | :--- | :---- | :--- | :--- | :--- |
| 10 | /28 (16 IPs) | 8 | 192.168.72.0/28 | 192.168.72.1-192.168.72.14 | 192.168.72.1 |
| 20 | /30 (4 IPs) | 2 | 192.168.72.16/30| 192.168.72.17-192.168.72.18| 192.168.72.17 |
| 30 | /28 (16 IPs) | 5 | 192.168.72.32/28| 192.168.72.33-192.168.72.46| 192.168.72.33 |
| 40 | /28 (16 IPs) | 8 | 192.168.72.48/28| 192.168.72.49-192.168.72.62| 192.168.72.49 |

-----

## Network Distribution

| VLAN | Name | Locations / Machines | Hosts |
| :--- | :--- | :--- | :--- |
| 10 | Administration | Office 3 (6-9), Office 6 (16-17), Meeting Room (22-23) | 8 |
| 20 | Common Areas | Corridor (1), Entrance/Exit (2) | 2 |
| 30 | Maintenance / Planning | Entrance/Exit (3), Office 4 (4-5), Office 5 (10-11) | 5 |
| 40 | Support (Marketing/Sales) | Office 1 (18-21), Office 2 (12-15) | 8 |

-----

## Installation Cost

### Cabling Infrastructure

  - **Cabling:** Category 6 (Cat6)
  - **Topology:** Cables run from a central rack to each room.
  - **Protection:** Cables are passed through closed metal or plastic trays.
  - **Average Distance (Rack to Room):** 20 meters
  - **Number of Racks:** 1 central rack
  - **Cabling Capacity:** 1 cable per point (24 total cables)

### Conduit and Cable Sizing

  - **Total Occupied Area:** 8 $cm^{2}$
  - **Recommended Maximum Conduit Use:** 40%
  - **Required Usable Area:** 8 $cm^{2}\div0.4 = 20~cm^{2}$
  - **Main Conduit Run:** 20 meters
  - **Branches:** 10 branches of 2 meters each
  - **Total Conduit Length:** $20+(10\times2)=40$ linear meters
  - **Number of Cables:** 40
  - **Average Cable Length:** 20 meters
  - **Total Cable:** $40\times20=800$ meters

### Budget

| Item | Qty. | Unit | Description | Price (R$) | Total (R$) |
| :--- | :--- | :--- | :--- | ---: | ---: |
| 1 | 1 | un | Switch Core | 30,000.00 | 30,000.00 |
| 2 | 54 | mt | 1/2 inch Conduit | 8.45 | 456.30 |
| 3 | 8 | un | 1/2" Threaded Conduit Bends | 10.80 | 86.40 |
| 4 | 2 | un | 3/4" T-Box | 18.50 | 37.00 |
| 5 | 3 | un | 3/4" L-Box | 18.50 | 55.50 |
| 6 | 7 | un | 1/4" Conduit Body with 2 passage entries | 17.90 | 125.30 |
| 7 | 26 | un | Conduit Body with 1 entry for network points | 17.90 | 465.40 |
| 8 | 25 | un | Type D-3/4 Clamp (Zinc-plated Carbon Steel) | 2.00 | 50.00 |
| 9 | 1 | un | 8U Rack | 975.00 | 975.00 |
| 10 | 1 | un | Cable Organizer | 52.00 | 52.00 |
| 11 | 1 | un | Cisco Router | 7,500.00 | 7,500.00 |
| 12 | 1 | un | DELL Server | 5,000.00 | 5,000.00 |
| 13 | 800 | mt | CAT6 Network Cable + Installation | 17.50 | 16,400.00 |
| | | | **GRAND TOTAL** | | **61,202.90**|

-----

## Network Port Identification (TIA-606 Standard)

| Port | TIA-606 ID | Location / Sector |
| :--- | :--- | :--- |
| FastEthernet0/1 | ED1/ER01/SW01/PT01 | Common Areas - Corridor |
| FastEthernet0/2 | ED1/ER01/SW01/PT02 | Common Areas - Entrance/Exit |
| FastEthernet0/3 | ED1/ER01/SW01/PT03 | Planning - Entrance/Exit |
| FastEthernet0/4 | ED1/ER01/SW01/PT04 | Planning - Office 4 |
| FastEthernet0/5 | ED1/ER01/SW01/PT05 | Planning - Office 4 |
| FastEthernet0/6 | ED1/ER01/SW01/PT06 | Administration - Office 3 |
| FastEthernet0/7 | ED1/ER01/SW01/PT07 | Administration - Office 3 |
| FastEthernet0/8 | ED1/ER01/SW01/PT08 | Administration - Office 3 |
| FastEthernet0/9 | ED1/ER01/SW01/PT09 | Administration - Office 3 |
| FastEthernet0/10 | ED1/ER01/SW01/PT10 | Planning - Office 5 |
| FastEthernet0/11 | ED1/ER01/SW01/PT11 | Planning - Office 5 |
| FastEthernet0/12 | ED1/ER01/SW01/PT12 | Support - Office 2 |
| FastEthernet0/13 | ED1/ER01/SW01/PT13 | Support - Office 2 |
| FastEthernet0/14 | ED1/ER01/SW01/PT14 | Support - Office 2 |
| FastEthernet0/15 | ED1/ER01/SW01/PT15 | Support - Office 2 |
| FastEthernet0/16 | ED1/ER01/SW01/PT16 | Administration - Office 6 |
| FastEthernet0/17 | ED1/ER01/SW01/PT17 | Administration - Office 6 |
| FastEthernet0/18 | ED1/ER01/SW01/PT18 | Support - Office 1 |
| FastEthernet0/19 | ED1/ER01/SW01/PT19 | Support - Office 1 |
| FastEthernet0/20 | ED1/ER01/SW01/PT20 | Support - Office 1 |
| FastEthernet0/21 | ED1/ER01/SW01/PT21 | Support - Office 1 |
| FastEthernet0/22 | ED1/ER01/SW01/PT22 | Administration - Meeting Room |
| FastEthernet0/23 | ED1/ER01/SW01/PT23 | Administration - Meeting Room |
| GigabitEthernet0/1| ED1/ER01/SW01/PTG1 | Trunk to External Router |

-----

## Device Configurations

### Cisco Router Configuration

```cisco
enable
configure terminal

! BGP Configuration
router bgp 65019

! VLAN Sub-interfaces
interface FastEthernet0/0
 no shutdown

interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.72.1 255.255.255.240
 no shutdown

interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.72.17 255.255.255.240
 no shutdown

interface FastEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.72.33 255.255.255.240
 no shutdown

interface FastEthernet0/0.40
 encapsulation dot1Q 40
 ip address 192.168.72.49 255.255.255.240
 no shutdown

! DHCP Pool for Administration VLAN
ip dhcp pool VLAN_ADMINISTRACAO
 network 192.168.72.0 255.255.255.240
 default-router 192.168.72.1
 dns-server 8.8.8.8
 exit

! DHCP Pool for Common Areas VLAN
ip dhcp pool VLAN_COMUM
 network 192.168.72.16 255.255.255.240
 default-router 192.168.72.17
 dns-server 8.8.8.8
 exit

! DHCP Pool for Planning VLAN
ip dhcp pool VLAN_PLANEJAMENTO
 network 192.168.72.32 255.255.255.240
 default-router 192.168.72.33
 dns-server 8.8.8.8
 exit

! DHCP Pool for Support VLAN
ip dhcp pool VLAN_APOIO
 network 192.168.72.48 255.255.255.240
 default-router 192.168.72.49
 dns-server 8.8.8.8
 exit

! Excluded DHCP Addresses
ip dhcp excluded-address 192.168.72.17 192.168.72.18
ip dhcp excluded-address 192.168.72.33 192.168.72.34
ip dhcp excluded-address 192.168.72.49 192.168.72.50

end
write memory
```

### Core Switch Configuration

```cisco
enable
configure terminal

! VLAN Creation
vlan 10
 name ADMINISTRACAO
 exit
vlan 20
 name COMUM
 exit
vlan 30
 name PLANEJAMENTO
 exit
vlan 40
 name APOIO
 exit

! Port Assignments for VLAN 10 (ADMINISTRACAO)
interface range FastEthernet0/6 - 9, FastEthernet0/16 - 17, FastEthernet0/22 - 23
 switchport mode access
 switchport access vlan 10
 no shutdown
 exit

! Port Assignments for VLAN 20 (COMUM)
interface range FastEthernet0/1 - 2
 switchport mode access
 switchport access vlan 20
 no shutdown
 exit

! Port Assignments for VLAN 30 (PLANEJAMENTO)
interface range FastEthernet0/3 - 5, FastEthernet0/10 - 11
 switchport mode access
 switchport access vlan 30
 no shutdown
 exit

! Port Assignments for VLAN 40 (APOIO)
interface range FastEthernet0/12 - 15, FastEthernet0/18 - 21
 switchport mode access
 switchport access vlan 40
 no shutdown
 exit

! Trunk Port Configuration
interface FastEthernet0/24
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40
 no shutdown
 exit

end
write memory
```
