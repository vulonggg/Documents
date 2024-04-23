> *(Bet2arab elBe3eed*

*W Betba3ad el2areeb Yaaaaaa 2asawtek)*

VLANs

> & Trunks
>
> **<u>Overview</u>**

- A full layer 2 only switched network is referred to as a single
  broadcast domain, so network must be subdivided into VLANs

- By definition a VLAN is a single broadcast domain, VLAN is

> characterised by:
>
> -They can allow load balancing with multiple parallel paths, so
> enhancing bandwidth utilization
>
> -They enhance network security
>
> -They confine broadcasts, so introducing better broadcast control
>
> -They can span multiple switches (no physical boundaries), VLAN can
> group users based on their business requirements (business
> departments) independent of any physical locations

- Segmentation

- Flexibility

- Security

> A VLAN = A Broadcast Domain = Logical Network (Subnet)
>
> But using VLANs will cause the following:

- It will not simplify the network.

- It will not eliminate the need of L3 routing

> **<u>Deploying VLANs</u>**

- The number of VLANS will be dependent on network requirement

- Cisco recommend the VLAN-IP relation to be one- to-one in order of
  isolating VLANs broadcasts & ability to form inter-VLAN-routing

- VLANs could be implemented using two basic methods

1)  Local VLANs

2)  End to End VLAN

> 1)Local VLAN

- It is called geographic VLANs, keeping the VLAN within a switch block

- Local VLANs are created based on geographic or physical locations

- Also Local VLANs design obey 20/80 rule

<img src="media/image42.jpeg" style="width:4.32265in;height:3.18229in"
alt="scl5" />

- Here are some local VLAN characteristics and user guidelines:

<!-- -->

- Local VLANs should be created with physical boundaries in mind rather
  than the job functions of the users on the end devices.

- Traffic from a local VLAN is routed to reach destinations on other
  networks.

- A single VLAN does not extend beyond the Building Distribution
  submodule.

> **<u>2)End to End VLAN</u>**

- It is called Campus-wide VLAN

- Users are assigned to VLANs regardless of their physical location,
  they are designed regarding their function (same VLAN are distributed
  on among different switch blocks)

- End to end VLAN disobey the 80/20 rule, where all traffic within a
  single VLAN could cross the core <u>obeying</u> 20/80 rule

- But end to end VLAN could help extending broadcast storms & it is
  difficult to maintain troubleshooting

- End to end VLAN deployment is not recommended by Cisco.

- <u>An end-to-end VLAN has these characteristics</u>:

  - The VLAN is geographically dispersed throughout the network.

  - Users are grouped into the VLAN regardless of physical location.

  - As a user moves throughout a campus, the VLAN membership of that

> user remains the same.

- Users are typically associated with a given VLAN for network
  management reasons.

- All devices on a given VLAN typically have addresses on the same IP
  subnet.

<img src="media/image51.jpeg" style="width:4.44629in;height:2.98646in"
alt="scl4" />

# Static VLAN membership

> **<u>VLAN membership</u>**
>
> ―Port based VLAN―
>
> VLAN number is assigned to specific switch port, each port gets a PVID
> (Port VLAN ID)

# Dynamic VLAN membership

> "MAC based VLAN"
>
> When a host is connected to a switch port, the switch must query a
> database to establish VLAN membership, so as to assign a MAC address
> of a user to a certain VLAN, a network administrator must assign the
> users MAC addresses to a VLAN in the database of VMPS (VLAN Membership
> Policy Server), which could be catalyst 6500/5000 or external server.
>
> **<u>Types of Switch ports</u>**

# Access-Link:

> -Switch port that is member in only one VLAN (native VLAN by default)
>
> -This port actually connect a switch to host

# Trunk-Link:

> -Switch port that is member in all VLANs by default, so traffic from
> all VLANs can use a trunk link
>
> -It is mainly used to connect two switches together or switch and a
> router
>
> To configure VLANs there are three requirements:
>
> **<u>Configuring VLANs</u>**

1.  Create VLAN

2.  Optionally name the VLAN

3.  Activate VLAN (assign VLAN to switchport)

> Method 1

Deleting VLAN

> Switch#configure terminal Switch(config)#no vlan 3 Switch(config)#end
>
> Switch#configure terminal Switch(config)#vlan 3
> Switch(config-vlan)#name sales Switch(config-vlan)#exit
> Switch(config)#
>
> \#configure terminal (config)#vlan \<id\>
>
> (config-vlan)#name \<vlan name\>
>
> Method 2: old IOS methods
>
> Alternatively, VLANs can be created and managed using VLAN database
> mode.

Deleting VLAN

> sw_2950#vlan database sw_2950(vlan)#vlan 9 name sales
> sw_2950(vlan)#exit
>
> APPLY completed. Exiting....
>
> sw_2950#
>
> \#vlan database
>
> (vlan)# vlan *vlan#* \[name *vlan-name*\] (vlan)#apply ,or (vlan)#exit
>
> Switch#vlan database
>
> Switch(vlan)#no vlan 3
>
> VLAN 3 deleted: Switch(vlan)#exit APPLY completed.
>
> Exiting....
>
> VLAN database mode is session oriented. When you add, delete, or
> modify VLAN parameters, the changes are not applied until you enter
> the apply or exit command. You can also exit VLAN database mode
> without applying the changes by entering the abort command.
>
> From this mode, you can add, delete, and modify VLAN configurations
> for VLANs
>
> in the range 1 to 1005.
>
> Note: This mode has been deprecated and will be removed in some future
> release.
>
> To activate a VLAN (config)#interface

50

> (config-if)#switchort mode access
>
> (config-if)#switchport access vlan \<vlan id\>
>
> (config)#interface Fastethernet 0/3 (config-if)#switchort mode access
> (config-if)#switchport access vlan 52
>
> Troubleshooting VLANs:
>
> Switch#show vlan \[id \| name\] *\[vlan_num* \| *vlan_name\]*

<table>
<colgroup>
<col style="width: 5%" />
<col style="width: 1%" />
<col style="width: 41%" />
<col style="width: 1%" />
<col style="width: 11%" />
<col style="width: 1%" />
<col style="width: 8%" />
<col style="width: 30%" />
</colgroup>
<thead>
<tr class="header">
<th colspan="8">#show vlan</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>VLAN</td>
<td></td>
<td>Name</td>
<td></td>
<td>Status</td>
<td></td>
<td>Ports</td>
<td></td>
</tr>
<tr class="even">
<td>- 1</td>
<td></td>
<td>default</td>
<td></td>
<td><blockquote>
<p>active</p>
</blockquote></td>
<td></td>
<td>Fa0/1,</td>
<td><blockquote>
<p>Fa0/2, Fa0/5, Fa0/7</p>
</blockquote></td>
</tr>
<tr class="odd">
<td>2</td>
<td></td>
<td>VLAN0002</td>
<td></td>
<td><blockquote>
<p>active</p>
</blockquote></td>
<td></td>
<td><blockquote>
<p>Fa0/8,</p>
<p>Gi0/1,</p>
</blockquote></td>
<td><blockquote>
<p>Fa0/9, Fa0/11, Fa0/12</p>
<p>Gi0/2</p>
</blockquote></td>
</tr>
<tr class="even">
<td><p>52</p>
<p>…</p></td>
<td></td>
<td>Sales</td>
<td></td>
<td><blockquote>
<p>active</p>
</blockquote></td>
<td></td>
<td>Fa0/3</td>
<td></td>
</tr>
<tr class="odd">
<td colspan="8">VLAN Type SAID MTU Parent RingNo BridgeNo Stp BrdgMode
Trans1 Trans2</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 6%" />
<col style="width: 1%" />
<col style="width: 6%" />
<col style="width: 1%" />
<col style="width: 12%" />
<col style="width: 1%" />
<col style="width: 6%" />
<col style="width: 1%" />
<col style="width: 45%" />
<col style="width: 1%" />
<col style="width: 7%" />
<col style="width: 1%" />
<col style="width: 7%" />
</colgroup>
<thead>
<tr class="header">
<th>1</th>
<th></th>
<th>enet</th>
<th></th>
<th><blockquote>
<p>100001</p>
</blockquote></th>
<th></th>
<th>1500</th>
<th></th>
<th>- - - - -</th>
<th></th>
<th>1002</th>
<th></th>
<th>1003</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2</td>
<td></td>
<td>enet</td>
<td></td>
<td><blockquote>
<p>100002</p>
</blockquote></td>
<td></td>
<td>1500</td>
<td></td>
<td>- - - - -</td>
<td></td>
<td>0</td>
<td></td>
<td>0</td>
</tr>
<tr class="even">
<td><blockquote>
<p>52</p>
</blockquote></td>
<td></td>
<td>enet</td>
<td></td>
<td><blockquote>
<p>100052</p>
</blockquote></td>
<td></td>
<td>1500</td>
<td></td>
<td>- - - - -</td>
<td></td>
<td>0</td>
<td></td>
<td>0</td>
</tr>
<tr class="odd">
<td>…</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

\#show vlan brief

VLAN Name

Status Ports

1

default

active

Fa0/1, Fa0/2, Fa0/5, Fa0/7

> Fa0/8, Fa0/9, Fa0/11, Fa0/12 Gi0/1, Gi0/2

2

> 52

VLAN0002

Sales

> active

active Fa0/3

1002 fddi-default

1003 token-ring-default

1004 fddinet-default

1005 trnet-default

active active active

active

> **<u>VLAN Trunks</u>**

- To connect switch port to another switch port or a router while
  deploying VLANs we need a method for VLAN Inter-switch communication
  where a VLAN can span multiple switches

- VLAN trunks will help for communication between same VLAN members that
  exist on different physical switches

Without trunking

With trunking

VLAN frame identifier

- Each frame originated from a PC and received on a switch port must
  have a VLAN id before retransmitted on a trunk link, this is called
  trunk VLAN tagging, this must be done to assure VLAN inter-switch
  communication.

- VLAN tagging types:

1.  ISL (Inter Switch Link) for Ethernet

2.  IEEE 802.1q (dot1q) for Ethernet

3.  Cisco extension for 802.10 for FDDI

4.  LANE (LAN Emulation) for ATM

- Cisco implements VLAN tagging

> using ASICs.

- It a Cisco proprietary VLAN tagging protocol,

> 1)ISL
>
> but it is no longer supported by Cisco new edge switches

- It is also called double tagging, because it encapsulates the original
  frame with new header (ISL header 26byte) &

> new trailer (ISL trailer 4byte new CRC)

- The ISL header contains a 10 bit for VLAN id,

> which support VLANs from 0-1023,
>
> where used VLANs are 1-1005

- Ethernet can use 1-1001 and 1002-1005 are reserved for token ring &
  FDDI

> Standard NIC cards and networking devices don’t understand this giant
> frame. A Cisco switch must remove this encapsulation before sending
> the frame out on an access link.

- ISL is now supported only on core switches, but Cisco Catalyst 2950 &
  2960 access switches support only dot1q.

> <img src="media/image254.png" style="width:0.74822in;height:0.255in" /><img src="media/image255.png" style="width:1.70447in;height:0.255in" /><img src="media/image256.png" style="width:0.7348in;height:0.255in" /><img src="media/image257.png" style="width:0.74822in;height:0.255in" /><img src="media/image258.png" style="width:2.29842in;height:0.455in" /><img src="media/image259.png" style="width:1.01664in;height:0.255in" /><img src="media/image260.png" style="width:0.91599in;height:0.255in" /><img src="media/image261.png" style="width:2.06349in;height:0.255in" /><img src="media/image262.png" style="width:1.01664in;height:0.255in" />**<u>2)dot1q</u>**

- It is called single tagging, where 4 byte of dot1q tag is inserted
  after the source MAC of the frame and before the length field of the
  frame

- The 4 bytes specify the following:

2-byte TPID (Tag Protocol Identifier)

2-byte TCI Tag Control Info (includes VLAN ID)

- 2 bytes for indication of type of encapsulated data

- 12 bit for VLAN tag, which give VLAN ranges from 0-4095, where
  0,1,1002-1005 & 4095 are reserved.

- 3 bits COS (Class Of Service), which indicates the priority of the
  frame, they are called the 802.1q/802.1p bits

- 1 bit for CFI (Canonical Frame Indicator), flag which indicates

> <img src="media/image273.png" style="width:0.92941in;height:0.255in" /><img src="media/image274.png" style="width:1.71118in;height:0.255in" /><img src="media/image275.png" style="width:0.76836in;height:0.255in" /><img src="media/image276.png" style="width:0.74822in;height:0.255in" /><img src="media/image277.png" style="width:1.18105in;height:0.255in" /><img src="media/image278.png" style="width:0.30197in;height:0.255in" />whether
> the frame is Ethernet or Token ring & FDDI

VLAN Ranges and Mappings

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>VLAN Range</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>0, 4095</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>1</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>2-1001</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>1002-1005</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>1025-4094</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>Range</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Reserved</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Normal</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Normal</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Normal</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Extended</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>Usage</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>For system use only</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Cisco default</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>For Ethernet VLANs</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Cisco defaults for FDDI and</p>
<p>Token Ring</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>For Ethernet VLANs only</p>
</blockquote></td>
</tr>
<tr class="even">
<td><strong>A</strong></td>
</tr>
</tbody>
</table>

- Dot1q also introduced the concept of native VLAN on a trunk,

> where frames belonging to this VLAN are not tagged with any VLAN id,
> using this feature 802.1q tagging device & non- 802.1q devices can
> co-exist on a 802.1q trunk.

- Native VLAN is by default VLAN 1, which is also called the management
  VLAN (management VLAN is the VLAN that carries frames from all
  protocols (CDP, VTP, DTP,….)), the native VLAN can be changed by
  configuration.

- IEEE 802.3ac standard is used to extended MTU of Ethernet frame to
  1522 byte

> NIC cards and networking devices can understand this “baby giant”
> frame (1522 bytes). However, a Cisco switch must remove this
> encapsulation before sending the frame out on an access link.

**<u>DTP</u>**

> **<u>(Dynamic Trunk Protocol)</u>**

- Cisco proprietary protocol, that is used to automatically negotiate a
  common trunking mode (negotiate whether link will be access or trunk)
  between two switches, also negotiation of trunk encapsulation type can
  be done, DTP negotiation is made periodically every 30 sec.

- A router can not participate in DTP, so if a switch port is connected
  to a router, DTP must be disabled & switch port must be manually
  configured.

- Note: DTP is negotiated between switches working in the same VTP
  domain or if one of these domains is null domain, so if switches are
  in different domains, you must set trunk configuration to "on" or

> 74 "nonegotiate", this setting will force the trunk to be established.
>
> <img src="media/image27.png" style="width:0.81in" />**AHMED NABIL**
>
> <img src="media/image289.png" /><img src="media/image302.png" style="width:4.06709in;height:0.525in" /><img src="media/image303.png" style="width:4.32in;height:0.76in" /><img src="media/image304.png" style="width:4.20997in;height:0.525in" /><img src="media/image307.png" style="width:4.47911in;height:0.525in" /><img src="media/image308.png" style="width:0.69727in;height:0.295in" />•
>
> **<u>DTP modes:</u>**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>Mode</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>access</p>
</blockquote></td>
</tr>
<tr class="even">
<td><blockquote>
<p>trunk</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>nonegotiate</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>dynamic desirable</p>
</blockquote></td>
</tr>
<tr class="even">
<td><blockquote>
<p>dynamic auto</p>
</blockquote></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>Function</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Unconditionally sets a switch port to access mode, regardless of
other DTP functions</p>
</blockquote></td>
</tr>
<tr class="even">
<td><blockquote>
<p>Sets the switch port to unconditional trunking mode</p>
<p>and negotiates to become a trunk link, regardless of neighbor
interface mode</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Specifies that DTP negotiation packets are not sent on the Layer 2
interface</p>
</blockquote></td>
</tr>
<tr class="even">
<td></td>
</tr>
<tr class="odd">
<td><blockquote>
<p>Sets the switch port to actively send and respond to DTP negotiation
frames. Default for Ethernet</p>
</blockquote></td>
</tr>
<tr class="even">
<td><blockquote>
<p>Sets the switch port to respond but not to actively</p>
<p>send DTP negotiation frames</p>
</blockquote></td>
</tr>
</tbody>
</table>

> **<u>Configuring trunking</u>**

(config)#interface \<\_\>

(config-if)#switchport mode {access/trunk/dynamic desirable/dynamic
auto/nonegotiate}

> -access: only in one VLAN, no negotiation (no DTP messages).
>
> <img src="media/image325.png" style="width:4.12358in;height:0.525in" />-trunk:
> permanently trunk & generate DTP messages.
>
> -dynamic desirable: (default), actively (sending messages) attempts to
> be
>
> trunk.
>
> -dynamic auto: only if far end desire a trunk, it will turn to trunk
> which means it is passively (does not initiate messages) attempts to
> be trunk.
>
> -nonegotiate: disables DTP & force permanent trunk.

(config-if)#switchport trunk encapsulation {isl/dot1q/negotiate}

> default is negotiate, ISL is favoured if both exist on negotiating
> switches.

Switchport Mode Interactions

<img src="media/image336.png"
style="width:5.59818in;height:2.51875in" />

# To identify native VLAN

**(config-if)#switchport trunk native vlan <u>\<vlan id\></u>**

> default is VLAN 1, this is used only with dot1q & trunking mode

# To specify allowed VLANs on trunk:

**(config-if)#switchport trunk allowed vlan {<u>\<vlan list\></u> / all
/**

> **{add/except/remove} <u>\<vlan list\></u> }**
>
> **Add: add VLAN list to an existing pre-configured list Except: means,
> all except a certain VLAN list Remove: remove VLANs from existing VLAN
> list**

By default all VLANs exist ion the trunk link.

> Trunking configuration example:
>
> Switch(config)#interface fastethernet 5/8 Switch(config-if)#switchport
> trunk encapsulation dot1q
>
> Switch(config-if)#switchport trunk allowed vlan 1,15,11,1002-1005
>
> Switch(config-if)#switchport mode trunk Switch(config-if)#no shutdown

Switch#show interfaces fastethernet 2/1 trunk

Port Fa2/1

VLANs allowed on trunk 1-1005

Port Fa2/1

VLANs allowed and active in management domain 1-2,1002-1005

Port Fa2/1

VLANs in spanning tree forwarding state and not pruned 1-2,1002-1005

\#sh dtp

\#sh interface \<\_\> trunk

**<u>Troubleshooting</u>**

\#sh interface \<\_\> switchport \#sh interface \<\_\> capabilities \#sh
run interface \<\_\>

\#sh vlan

\#sh vlan brief

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 21%" />
<col style="width: 25%" />
<col style="width: 18%" />
<col style="width: 22%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p>Port</p>
</blockquote></th>
<th><blockquote>
<p>Mode</p>
</blockquote></th>
<th><blockquote>
<p>Encapsulation</p>
</blockquote></th>
<th><blockquote>
<p>Status</p>
</blockquote></th>
<th><blockquote>
<p>Native VLAN</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Fa2/1</p>
</blockquote></td>
<td><blockquote>
<p>desirable</p>
</blockquote></td>
<td><blockquote>
<p>isl</p>
</blockquote></td>
<td><blockquote>
<p>trunking</p>
</blockquote></td>
<td><blockquote>
<p>1</p>
</blockquote></td>
</tr>
</tbody>
</table>

> Switch#show interfaces gigabitEthernet 0/1 switchport Name: Gi0/1
>
> Switchport: Enabled Administrative Mode: trunk Operational Mode: trunk
>
> Administrative Trunking Encapsulation: dot1q Operational Trunking
> Encapsulation: dot1q Negotiation of Trunking: On
>
> Access Mode VLAN: 1 (default)
>
> Trunking Native Mode VLAN: 1 (default)
>
> Trunking VLANs Enabled: ALL Pruning VLANs Enabled: 2-1001
>
> . . .

# Troubleshooting VLAN Issues

> Configuration problems can arise when user traffic must traverse
> several switches. The following sections list some common
> configuration errors. But before you begin troubleshooting, create a
> plan. Check the implementation plan for any changes recently made, and
> determine likely problem areas.

# Troubleshooting User Connectivity

> User connectivity can be affected by several things:

- **Physical connectivity:** Make sure the cable, network adapter, and
  switch

> port are good. Check the port’s link LED.

- **Switch configuration**: If you see FCS errors or late collisions,
  suspect a duplex mismatch. Check configured speed on both sides of the
  link. Make sure the port is enabled and set as an access port.

- **VLAN configuration:** Make sure the hosts are in the correct VLAN.

- **Allowed VLANs:** Make sure that the user VLAN is allowed on all
  appropriate trunk links.

# Troubleshooting Trunking

> When troubleshooting trunking, make sure that physical layer
> connectivity is present before moving on to search for configuration
> problems such as

- Are both sides of the link in the correct trunking mode?

- Is the same trunk encapsulation on both sides?

- If 802.1Q, is the same native VLAN on both sides? Look for CDP
  messages

> warning of this error.

- Are the same VLANs permitted on both sides?

- Is a link trunking that should not be?

https://viblo.asia/p/vlan-la-gi-vlan-trunking-protocol-la-gi-bXP4WzeYV7G#\_31-dung-moi-ket-noi-cho-tung-vlan-5

https://www.totolink.vn/article/97-vtp-la-gi-vlan-trunking-protocol-la-gi.html

https://blog.cloud365.vn/windows/linux/other/huong-dan-cau-hinh-vlan-trunking/
