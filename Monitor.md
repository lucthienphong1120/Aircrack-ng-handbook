# Monitor mode

## Check mode status

```
sudo iw dev
or
sudo iwconfig
or
sudo airmon-ng
```

![image](https://user-images.githubusercontent.com/90561566/163700017-5f40f0f8-1b37-498e-8b0f-7f7fe3a75cdc.png)

## Enable monitor mode

### Method 1: Using ip link set

```
sudo ip link set <IFACE> down
sudo iw <IFACE> set monitor control
sudo ip link set <IFACE> up
```

Check again

![image](https://user-images.githubusercontent.com/90561566/163700066-5f59de42-3486-4baa-a9f2-8860bfdef11a.png)

If you want get back to the Managed Mode

```
sudo ip link set <IFACE> down
sudo iw <IFACE> set type managed
sudo ip link set <IFACE> up
service NetworkManager restart
```

### Method 2: Using iwconfig

```
sudo ifconfig <IFACE> down
sudo iwconfig <IFACE> mode monitor
sudo ifconfig <IFACE> up
```

If you want get back to the Managed Mode

```
sudo ifconfig <IFACE> down
sudo iwconfig <IFACE> mode managed
sudo ifconfig <IFACE> up
service NetworkManager restart
```

### Method 3: Using airmon-ng

```
sudo airmon-ng check kill
sudo airmon-ng start <IFACE>
```

![image](https://user-images.githubusercontent.com/90561566/163700327-50af7b2f-188c-44e4-8c54-3afc132dc065.png)

It will create wlan0mon

![image](https://user-images.githubusercontent.com/90561566/163700331-65ed4e79-cf88-4cbd-b8b2-1763a5f8c938.png)

If you want get back to the Managed Mode

```
sudo airmon-ng stop <IFACE>
service NetworkManager restart
```

# Aircrack-ng

Start crack wifi with [Aircrack-ng.md](/Aircrack-ng.md)


















