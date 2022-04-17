# Aircrack-ng-experience

## Setup usb wifi

I use tp-link wn725n (chip set rtl8188eus)

### Check connect:

```
ifconfig
iwconfig
```

![image](https://user-images.githubusercontent.com/90561566/163680598-fff970c5-959a-45f5-a0f5-d448f5b712e1.png)

### Setup OS:

See this: 
- Command: https://github.com/davidbombal/Kali-Linux/blob/main/TP-Link%20TL-WN722N%20adapter
- Setup: https://github.com/aircrack-ng/rtl8188eus
- Tool setup: https://github.com/sonvan1811/rtl8188eus

### Linux header:

```
sudo apt-get clean
sudo apt-get update
sudo apt-get upgrade
```

1) Method 1: Run the following command to install the kernel header file.

```
sudo apt-get install linux-headers-$(uname -r)
```

![image](https://user-images.githubusercontent.com/90561566/163698546-a9e3bfe8-380c-4e02-b365-09b9649436eb.png)

2) Method 2: Manually Download and Compile to Install

Check the system version of Kali
```
uname -r
```



### See information:

```
lsusb
lsusb -D /dev/bus/usb/<bus>/<device>
```

![image](https://user-images.githubusercontent.com/90561566/163680503-3f9c38f0-185e-4144-bef9-0c694020c3e7.png)

### Check mode status

```
iw dev
```

![image](https://user-images.githubusercontent.com/90561566/163680743-8684357c-ae0b-4d04-a7a2-f06d1aea7d4d.png)







## aircrack
