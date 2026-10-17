# Static route config basics
## Objective: to configure ROAS on R1 such that VLAN traffic can be reached and Switches are properly configured with access/ trunkports

**details in screenshot**

![](images/13_ROAS_Config/ROAS1.png)


1. *to configure the switch interfaces as access ports we can do the following*

``
SW1> en
SW1# conf t
SW1(config)# int range f0/1-4
SW1(config-if)# switchport mode access
``

``
SW2> en
SW2# conf t
SW2(config)# int range f0/1-3
SW2(config-if)# switchport mode access
``


2. *then to assign VLAN10, VLAN30 to corresponding ports on SW1; VLAN10, VLAN20 to corresponding ports on SW2*

``
SW1(config-if)# int range f0/1-2
SW1(config-if)# switchport access vlan 10
SW1(config-if)# int range f0/3-4
SW1(config-if)# switchport access vlan 30
``

``
SW2(config-if)# int range f0/1
SW2(config-if)# switchport access vlan 20
SW2(config-if)# int range f0/2-3
SW2(config-if)# switchport access vlan 10
``

![](images/13_ROAS_Config/ROAS2.png)

![](images/13_ROAS_Config/ROAS3.png)


3. *now to configure the trunk ports g0/1 of SW1 and SW2, allow necessary VLANs only and use a different port for the native VLAN*

## SW2
``
SW2(config)# int g0/1
SW2(config-if)# switchport mode trunk
SW2(config-if)# switchport trunk allowed vlan 10,30
SW2(config-if)# switchport trunk native vlan 99
``

*keeping in mind that SW2 doesn't have VLAN30 connected so will need to create VLAN30 on SW2

``
SW2(config)#vlan 30
``
## SW1
``
SW1(config)# int g0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,30
SW1(config-if)# switchport trunk native vlan 99
``

![](images/13_ROAS_Config/ROAS4.png)

![](images/13_ROAS_Config/ROAS5.png)


4. Finally to configure R1's interface as ROAS and match the dot1q encapsulations with corresponding VLAN messages

``
R1(config)# int g0/0
R1(config-if)# no shutdown
R1(config-if)# int g0/0.10
R1(config-subif)# encapsulation dot1q 10
R1(config-subif)# ip address 10.0.0.62 255.255.255.192
R1(config-if)# int g0/0.2
R1(config-subif)# encapsulation dot1q 20
R1(config-subif)# ip address 10.0.0.126 255.255.255.192
R1(config-if)# int g0/0.3
R1(config-subif)# encapsulation dot1q 30
R1(config-subif)# ip address 10.0.0.190 255.255.255.192
``
# Also to remember to configure SW2's g0/2 interface as trunk
``
SW2(config)# int g0/2
SW2(config-if)# switchport mode trunk
``

![](images/13_ROAS_Config/ROAS6.png)


5. **resulting ping from PC3 to device in VLAN10 and VLAN20**

![](images/13_ROAS_Config/ROAS7.png)

*successful pings both times*
