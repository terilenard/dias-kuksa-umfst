# Dias Kuksa Instalation

## Requirements

Board: Raspberry pi 3 model B

System: Rasbian Buster 5.10.17

python version 3.7.3

## Before Instalation

```
$ sudo apt update
$ sudo apt upgrade 
$ sudo apt install git
```

## Virtual CAN Interface

Creating and setting up the virtual can interface
```
$ sudo modprobe vcan
$ sudo ip link add dev vcan0 type vcan
$ sudo ip link set up vcan0
```

To make it persistent, add the following lines in __/etc/network/interfaces__
```
auto vcan0
   iface vcan0 inet manual
   pre-up /sbin/ip link add dev $IFACE type vcan
   up /sbin/ifconfig $IFACE up
```
And in __/etc/modules__ add the line: 
```
vcan
```
finally, restart networking service:
```
sudo /etc/init.d/networking restart
```
The interface should be visible with __ifconfig__.
