# Monitor mode

## Check mode status

```
sudo iw dev
```

![image](https://user-images.githubusercontent.com/90561566/163700017-5f40f0f8-1b37-498e-8b0f-7f7fe3a75cdc.png)

## Enable monitor mode

### Method 1: Switch iw to Monitor Mode

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
```
