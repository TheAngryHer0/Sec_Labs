# SVI config on Multilayer switches
## Objective: to configure SVIs on Multilayer switch such that VLAN traffic can be reached

**Network toplogy; trunk, switchports and vlans already preconfigured to be same as ROAS_config lab**

![](images/15_MultilayerSwitching/L3switch_01.png)


1. *to replace the ROAS config on R1 and assign point to point ip address to g0/0*

![](images/14_ROAS_Config/ROAS6.png)

![](images/15_MultilayerSwitching/L3switch_03.png)


2. *Converting SW2 into multilayer switch and g1/0/2 into L3 port*

```
SW2(config)# ip routing
SW2(config)# int g1/0/2
SW2(config-if)# no switchport
```

![](images/15_MultilayerSwitching/L3switch_04.png)


3. *Also creating a default route for the nonspecific addresses*

```
SW2(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.194
```

![](images/15_MultilayerSwitching/L3switch_05.png)


4. *Checking VLAN status on SW2 then creating SVIs that are assigned with last usable ip address of each vlan*

![](images/15_MultilayerSwitching/L3switch_02.png)

```
SW2(config)# int vlan10
SW2(config-if)# ip address 10.0.0.62 255.255.255.192
SW2(config)# int vlan20
SW2(config-if)# ip address 10.0.0.126 255.255.255.192
SW2(config)# int vlan30
SW2(config-if)# ip address 10.0.0.190 255.255.255.192
```

![](images/15_MultilayerSwitching/L3switch_06.png)


5. *SW2 routing table*

![](images/15_MultilayerSwitching/L3switch_10.png)


6. *testing connectivity between inter-vlan host machines*

## VLAN30 - VLAN10
![](images/15_MultilayerSwitching/L3switch_07.png)

## VLAN20 - VLAN30
![](images/15_MultilayerSwitching/L3switch_08.png)

## to "internet" (default route)
![](images/15_MultilayerSwitching/L3switch_09.png)


*successful pings to all destinations*

