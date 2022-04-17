# Aircrack-ng Experience

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

Example: 5.15.0-kali3-amd64

![image](https://user-images.githubusercontent.com/90561566/163698742-5110bbca-0f01-4fd1-a8bc-cd4787a1e30c.png)

Go to one of the following link:
- http://kali.download/kali/pool/main/l/linux/
- http://http.kali.org/kali/pool/main/l/linux/

Ctrl+F and find `linux-kbuild-` + `5.15_5.15` + xxxxxx + `amd64.deb` (choose the appropriate version you need)

![image](https://user-images.githubusercontent.com/90561566/163698880-60c0bf39-723c-4aed-8584-6424997e7f61.png)

xxxxxx here is `.15-1kali2_`

Ctrl+F and find `linux-headers-` + `5.15.0-` + `kali3-` + `common_` + `5.15_5.15` + xxxxxx + `_all.deb` (choose the appropriate version you need)

![image](https://user-images.githubusercontent.com/90561566/163698996-ac108a0b-95f0-4d85-b664-e1bcf640399c.png)




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
