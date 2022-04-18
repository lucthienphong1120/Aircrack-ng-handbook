# Setup usb wifi

I use tp-link wn725n (chip set rtl8188eus)

### Is your wifi support monitor mode ?

```
iw dev
iw phy phy0 info
```

Here will show all your wifi card parameters

![image](https://user-images.githubusercontent.com/90561566/163820140-91bfaa6a-0382-47f5-b075-8c07fc9a0778.png)

### Check connect:

```
ifconfig
iwconfig
```

![image](https://user-images.githubusercontent.com/90561566/163680598-fff970c5-959a-45f5-a0f5-d448f5b712e1.png)

### See information:

```
lsusb
lsusb -D /dev/bus/usb/<bus>/<device>
```

![image](https://user-images.githubusercontent.com/90561566/163680503-3f9c38f0-185e-4144-bef9-0c694020c3e7.png)

### Setup OS:

You can refer to the following links:

- Command Install: https://github.com/davidbombal/Kali-Linux/blob/main/TP-Link%20TL-WN722N%20adapter
- Install Driver: https://github.com/aircrack-ng/rtl8188eus
- Tool Auto Install: https://github.com/lucthienphong1120/rtl8188eus

### Linux header:

First, update the OS
```
sudo apt update
sudo apt upgrade
sudo apt-get dist-upgrade
reboot
```

1) Method 1: Run the following command to install the kernel header file.

```
sudo apt-get install linux-headers-$(uname -r)
```

After running this command, the system will automatically find the matched kernel header
file to download and install it. If the Kali server is updated, you may not find the specific file,
in this case, you can manually download and install the header file.

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

Ctrl+F and find `linux-kbuild-` + `5.15` + `_5.15` + xxxxxx + `amd64.deb` (choose the appropriate version you need)

![image](https://user-images.githubusercontent.com/90561566/163698880-60c0bf39-723c-4aed-8584-6424997e7f61.png)

xxxxxx here is `.15-1kali2_`

Ctrl+F and find `linux-headers-` + `5.15.0-kali3-amd64` + `_5.15` + xxxxxx + `_amd64.deb` (choose the appropriate version you need)

![image](https://user-images.githubusercontent.com/90561566/163699304-4a5e0161-9274-4393-9f1e-4f95c6a50948.png)

Maybe you will need `linux-compiler-gcc-11-x86`

![image](https://user-images.githubusercontent.com/90561566/163699463-8ed7cfe5-6bf4-4460-bcae-4a4556e1ba49.png)

Go to download directory

```
sudo dpkg -i linux-kbuild......
sudo dpkg -i linux-compiler......
sudo dpkg -i linux-headers.....
dpkg-query -s linux-headers-$(uname -r)
```

![image](https://user-images.githubusercontent.com/90561566/163699497-19fe1c40-d6a9-4f27-9e87-3a5314ec9b5f.png)

Check the `/lib/modules/<kernel-version>/` directory and you will see a build link file
  
![image](https://user-images.githubusercontent.com/90561566/163699535-d7d246b5-8c2b-4912-b7fd-d49052ee3ac8.png)

### Compile driver

Go to the driver directory (rtl8188eus with me). Run the following commands to compile the driver.

```
make all
make install
```

If success, you can will a name of the `<chip>`.ko file is stored in there.

### Load the Driver

```
sudo apt install bc
sudo apt-get install build-essential
sudo apt-get install libelf-dev
sudo apt install dkms
```

```
sudo rmmod r8188eu.ko
git clone https://github.com/aircrack-ng/rtl8188eus
cd rtl8188eus
sudo -i
echo 'blacklist r8188eu' | sudo tee -a '/etc/modprobe.d/realtek.conf'
exit
reboot
```

```
cd rtl8188eus
sudo make && make install
reboot
```

## Monitor mode

Go to [monitor.md](/Monitor.md)






