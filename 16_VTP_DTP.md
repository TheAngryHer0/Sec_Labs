# DTP/VTP config on switches
## Objective: to configure understand how VTP and DTP function on switches for scalable configuration

**Network toplogy including objectives listed**

![](images/16_VTP_DTP/VTP01.png)


1. *to configure the switchports connecting switches as trunkports while disabling dtp with nonegotiate for best practice*

```
SW1(config)# int g0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# swtichport nonegotiate
```

![](images/16_VTP_DTP/VTP02.png)

## Now similarly, for SW2 and SW3

![](images/16_VTP_DTP/VTP03.png)

![](images/16_VTP_DTP/VTP04.png)

## Confirming operational mode of SW1

![](images/16_VTP_DTP/VTP05.png)


2. *Configure SW1 in VTP domain CCNA, creating VLANs 10-30*

```
SW1(config)# vtp domain CCNA
SW1(config)# vlan10
SW1(config)# vlan20
SW1(config)# vlan30
SW1(config)# show vtp status
SW1(config)# show vlan
```

![](images/16_VTP_DTP/VTP06.png)

## VLANs on SW1

![](images/16_VTP_DTP/VTP06.png)


3. *Checking SW2 output while also configuring SW2 in transparent mode and adding VLAN40*

```
SW2(config)# vtp domain CCNA
SW2(config)# vtp mode transparent
```

![](images/16_VTP_DTP/VTP09.png)

## VLANs on SW2

![](images/16_VTP_DTP/VTP08.png)

*Configure SW2 is in transparent mode, so adding VLANs does not affect SW1 in server mode*


4. *Configuring SW3 in client mode and adding checking output*

```
SW2(config)# vtp domain CCNA
SW2(config)# vtp mode client
```

![](images/16_VTP_DTP/VTP10.png)

## VLANs on SW3

![](images/16_VTP_DTP/VTP11.png)

##Trying to add VLAN 50

![](images/16_VTP_DTP/VTP11.png)

*Adding VLAN numbers aren't allowed in client mode*


6. *converting all host connected ports to static access ports*

```
SW1(config)# int range f0/1-2
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport nonegotiate
```

*example output on SW1's f0/1 interface after doing this on all other switches*

```
SW1# show interfaces f0/1 switchport
```

![](images/16_VTP_DTP/VTP16.png)


*negotiation of trunking: off*

```
SW1# show vtp
```

## SW1

![](images/16_VTP_DTP/VTP13.png)

## SW2

![](images/16_VTP_DTP/VTP14.png)

## SW3

![](images/16_VTP_DTP/VTP15.png)


*confirming that changing to static switchport disables trunking and by extension DTP on those ports*

