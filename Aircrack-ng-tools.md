# [Aircrack-ng](https://www.aircrack-ng.org/) tools

## Sơ lược

Aircrack-ng là bộ công cụ dùng để pentest mạng không dây, crack wep và dò khóa wpa/wpa2-psk.

Aircrack-ng có rất nhiều công cụ, một số là:

### [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)

dùng để chuyển card mạng của bạn từ manager sang monitor

Enable monitor mode, kill network managers, go back managed mode, show the interfaces status

```
airmon-ng <start|stop> <interface> [channel] or airmon-ng <check|check kill>
```

### [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)

dùng để bắt gói tin trong mạng wifi

Detected access points, packet capture, capturing raw 802.11 frames, collecting WEP IVs or WPA handshakes, log the coordinates

```
airodump-ng <options> <interface>[,<interface>,...]
```

<details>
<summary>More</summary>

```
Options:
    --ivs                 : Save only captured IVs
    --gpsd                : Use GPSd
    --write      <prefix> : Dump file prefix
    -w                    : same as --write 
    --beacons             : Record all beacons in dump file
    --update       <secs> : Display update delay in seconds
    --showack             : Prints ack/cts/rts statistics
    -h                    : Hides known stations for --showack
    -f            <msecs> : Time in ms between hopping channels
    --berlin       <secs> : Time before removing the AP/client
                            from the screen when no more packets
                            are received (Default: 120 seconds)
    -r             <file> : Read packets from that file
    -T                    : While reading packets from a file,
                            simulate the arrival rate of them
                            as if they were "live".
    -x            <msecs> : Active Scanning Simulation
    --manufacturer        : Display manufacturer from IEEE OUI list
    --uptime              : Display AP Uptime from Beacon Timestamp
    --wps                 : Display WPS information (if any)
    --output-format
                <formats> : Output format. Possible values:
                            pcap, ivs, csv, gps, kismet, netxml, logcsv
    --ignore-negative-one : Removes the message that says
                            fixed channel <interface>: -1
    --write-interval
                <seconds> : Output file(s) write interval in seconds
    --background <enable> : Override background detection.
    -n              <int> : Minimum AP packets recv'd before
                            for displaying it
Filter options:
    --encrypt   <suite>   : Filter APs by cipher suite
    --netmask <netmask>   : Filter APs by mask
    --bssid     <bssid>   : Filter APs by BSSID
    --essid     <essid>   : Filter APs by ESSID
    --essid-regex <regex> : Filter APs by ESSID using a regular
                            expression
    -a                    : Filter unassociated clients

By default, airodump-ng hop on 2.4GHz channels.
You can make it capture on other/specific channel(s) by using:
    --ht20                : Set channel to HT20 (802.11n)
    --ht40-               : Set channel to HT40- (802.11n)
    --ht40+               : Set channel to HT40+ (802.11n)
    --channel <channels>  : Capture on specific channels
    --band <abg>          : Band on which airodump-ng should hop
    -C    <frequencies>   : Uses these frequencies in MHz to hop
    --cswitch  <method>   : Set channel switching method
                  0       : FIFO (default)
                  1       : Round Robin
                  2       : Hop on last
    -s                    : same as --cswitch

    --help                : Displays this usage screen
```

</details>

### [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)

dùng để tạo ra gói tin inject gửi tới AP nhằm nhận các gói ARP phản hồi.

Generate traffic, deauthentications, fake authentications, Interactive packet replay, hand-crafted ARP request injection and ARP-request reinjection,...

```
aireplay-ng <options> <interface>
```

<details>
<summary>More</summary>

```
Filter options:

    -b bssid : MAC address, Access Point
    -d dmac : MAC address, Destination
    -s smac : MAC address, Source
    -m len : minimum packet length
    -n len : maximum packet length
    -u type : frame control, type field
    -v subt : frame control, subtype field
    -t tods : frame control, To DS bit
    -f fromds : frame control, From DS bit
    -w iswep : frame control, WEP bit

Replay options:

    -x nbpps : number of packets per second
    -p fctrl : set frame control word (hex)
    -a bssid : set Access Point MAC address
    -c dmac : set Destination MAC address
    -h smac : set Source MAC address
    -e essid : For fakeauth attack or injection test, it sets target AP SSID. This is optional when the SSID is not hidden.
    -j : arpreplay attack : inject FromDS pkts
    -g value : change ring buffer size (default: 8)
    -k IP : set destination IP in fragments
    -l IP : set source IP in fragments
    -o npckts : number of packets per burst (-1)
    -q sec : seconds between keep-alives (-1)
    -y prga : keystream for shared key auth
    -B –-bittest : bit rate test (Applies only to test mode)
    -D :disables AP detection. Some modes will not proceed if the AP beacon is not heard. This disables this functionality.
    -F –-fast : chooses first matching packet. For test mode, it just checks basic injection and skips all other tests.
    -R disables /dev/rtc usage. Some systems experience lockups or other problems with RTC. This disables the usage.

Source options:

    iface : capture packets from this interface
    -r file : extract packets from this pcap file

Attack modes (Numbers can still be used):

    --deauth count : deauthenticate 1 or all stations (-0)
    --fakeauth delay : fake authentication with AP (-1)
    --interactive : interactive frame selection (-2)
    --arpreplay : standard ARP-request replay (-3)
    --chopchop : decrypt/chopchop WEP packet (-4)
    --fragment : generates valid keystream (-5)
    --test : injection test (-9)
```

</details>
    
## [Airbase-ng](https://www.aircrack-ng.org/doku.php?id=airbase-ng)              
                    
tạo điểm truy cập giả mạo
Caffe Latte WEP client attack, Hirte WEP client attack, WPA/WPA2 handshake, act as an ad-hoc Access Point, act as a full Access Point,...

```
airbase-ng <options> <replay interface>
```
                    
<details>
<summary>More</summary>
    
```
Options:

    -a bssid : set Access Point MAC address
    -i iface : capture packets from this interface
    -w WEP key : use this WEP key to encrypt/decrypt packets
    -h MAC : source mac for MITM mode
    -f disallow : disallow specified client MACs (default: allow)
    -W 0|1 : [don't] set WEP flag in beacons 0|1 (default: auto)
    -q : quiet (do not print statistics)
    -v : verbose (print more messages) (long --verbose)
    -M : M-I-T-M between [specified] clients and bssids (NOT CURRENTLY IMPLEMENTED)
    -A : Ad-Hoc Mode (allows other clients to peer) (long --ad-hoc)
    -Y in|out|both : external packet processing
    -c channel : sets the channel the AP is running on
    -X : hidden ESSID (long --hidden)
    -s : force shared key authentication
    -S : set shared key challenge length (default: 128)
    -L : Caffe-Latte attack (long --caffe-latte)
    -N : Hirte attack (cfrag attack), creates arp request against wep client (long –cfrag)
    -x nbpps : number of packets per second (default: 100)
    -y : disables responses to broadcast probes
    -0 : set all WPA,WEP,open tags. can't be used with -z & -Z
    -z type : sets WPA1 tags. 1=WEP40 2=TKIP 3=WRAP 4=CCMP 5=WEP104
    -Z type : same as -z, but for WPA2
    -V type : fake EAPOL 1=MD5 2=SHA1 3=auto
    -F prefix : write all sent and received frames into pcap file
    -P : respond to all probes, even when specifying ESSIDs
    -I interval : sets the beacon interval value in ms
    -C seconds : enables beaconing of probed ESSID values (requires -P)

Filter options:

    --bssid <MAC> : BSSID to filter/use (short -b)
    --bssids <file> : read a list of BSSIDs out of that file (short -B)
    --client <MAC> : MAC of client to accept (short -d)
    --clients <file> : read a list of MACs out of that file (short -D)
    --essid <ESSID> : specify a single ESSID (short -e)
    --essids <file> : read a list of ESSIDs out of that file (short -E)
```
    
</details>
                    
## [Packetforge-ng](https://www.aircrack-ng.org/doku.php?id=packetforge-ng)

dùng để gửi các gói tin giả trên tới AP để nhận phản hồi.

Create encrypted packets such as arp requests, UDP, ICMP and custom packets

```
packetforge-ng <mode> <options>
```
                    
<details>
<summary>More</summary>

```
Forge options

    -p <fctrl> : set frame control word (hex)
    -a <bssid> : set Access Point MAC address
    -c <dmac> : set Destination MAC address
    -h <smac> : set Source MAC address
    -j : set FromDS bit
    -o : clear ToDS bit
    -e : disables WEP encryption
    -k <ip[:port]> : set Destination IP [Port]
    -l <ip[:port]> : set Source IP [Port] (Dash lowercase letter L)
    -t ttl : set Time To Live
    -w <file> : write packet to this pcap file

Source options

    -r <file> : read packet from this raw file
    -y <file> : read PRGA from this file

Modes
    --arp : forge an ARP packet (-0)
    --udp : forge an UDP packet (-1)
    --icmp : forge an ICMP packet (-2)
    --null : build a null packet (-3)
    --custom : build a custom packet (-9)
```

</details>

## [Airolib-ng](https://www.aircrack-ng.org/doku.php?id=airolib-ng)

tạo ra một cơ sở dữ liệu khóa đã được tính toán trước, làm đơn giản hóa quá trình crack key

Store and manage essid and password lists, compute PMKs, WPA/WPA2 cracking

```
airolib <database> <operation> [options]
```
      
<details>
<summary>More</summary>

```
Operations:

    --stats - Output some information about the database.
    --sql {sql} - Execute the specified SQL statement.
    --clean [all] - Perform steps to clean the database from old junk. The option 'all' will also reduce file size if possible and run an integrity check.
    --batch - Start batch-processing all combinations of ESSIDs and passwords. This must be run prior to using the database within aircrack-ng or after you have added additional SSIDs or passwords.
    --verify [all] - Verify a set of randomly chosen PMKs. If the option 'all' is given, all(!) PMKs in the database are verified and the incorrect ones are deleted.
    --export cowpatty {essid} {file} - Export to a cowpatty file.
    --import cowpatty {file} - Import a cowpatty file and create the database if it does not exist.
    --import {essid|passwd} {file} - Import a text flat file as a list of either ESSIDs or passwords and create the database if it does not exist. This file must contain one essid or password per line. Lines should be terminated with line feeds. Meaning press "enter" at the end of each line when entering the values.
```

</details>
    
## [Airoscript-ng](https://www.aircrack-ng.org/doku.php?id=airoscript-ng)    

tự động hóa mọi công đoạn, bạn chỉ việc đưa vào mac AP, chọn kiểu tấn công và ngồi chờ

interface to interact with Aicrack-ng and easy WEP and WPA networks attacks, allow to save time from writing commands
    
```
airoscript-ng [options]
```
    
<details>
<summary>More</summary>
  
```
Options
    
    -t	terminal	Specify terminal (xterm or screen)
    -c	none	Launches an interface selection menu (requires -pzenity)
    -w	wireless_card	Specify wifi card
    -b	file	Writes a csv file with network data
    -m	mac_mode	Change mac to fakemac before everything else. (mac_mode = fakemac or realmac)
    -a	none	Automatic mode
    -n	regex	Filter SSID by regex
    -x	none	Autoconfigure network after automatic crack (requires -a)
    -z	none	Don't scan automatically at start
    -p	plugin file	Load plugin at start
    -v	none	Verbose & debug mode
    -h	none	Displays this usage screen
```
    
</details>
    
## [Aircrack-ng](https://www.aircrack-ng.org/doku.php?id=aircrack-ng)

crack wep hay dò khóa đều dùng nó

Aircrack-ng is an 802.11 WEP and WPA/WPA2-PSK key cracking program.

```
aircrack-ng [options] <capture file(s)>
```
    
<details>
<summary>More</summary>
    
```
Common options

    -a	amode	Force attack mode (1 = static WEP, 2 = WPA/WPA2-PSK)
    -e	essid	If set, all IVs from networks with the same ESSID will be used. This option is also required for WPA/WPA2-PSK cracking if the ESSID is not broadcasted (hidden)
    -b	bssid	Long version --bssid. Select the target network based on the access point's MAC address
    -p	nbcpu	On SMP systems: # of CPU to use. This option is invalid on non-SMP systems
    -q	Enable quiet mode (no status output until the key is found, or not)
    -C	MACs	Long version --combine. Merge the given APs (separated by a comma) into virtual one
    -l	file name	(Lowercase L, ell) logs the key to the file specified. Overwrites the file if it already exists
    
Static WEP cracking options

    -c	Restrict the search space to alpha-numeric characters only (0x20 - 0x7F)
    -t	Restrict the search space to binary coded decimal hex characters
    -h	Restrict the search space to numeric characters (0x30-0x39) These keys are used by default in most Fritz!BOXes
    -d	start	Long version --debug. Set the beginning of the WEP key (in hex), for debugging purposes
    -m	maddr	MAC address to filter WEP data packets. Alternatively, specify -m ff:ff:ff:ff:ff:ff to use all and every IVs, regardless of the network
    -n	nbits	Specify the length of the key: 64 for 40-bit WEP, 128 for 104-bit WEP, etc. The default value is 128
    -i	index	Only keep the IVs that have this key index (1 to 4). The default behaviour is to ignore the key index
    -f	fudge	By default, this parameter is set to 2 for 104-bit WEP and to 5 for 40-bit WEP. Specify a higher value to increase the bruteforce level: cracking will take more time, but with a higher likelyhood of success
    -k	korek	There are 17 korek statistical attacks. Sometimes one attack creates a huge false positive that prevents the key from being found, even with lots of IVs. Try -k 1, -k 2, … -k 17 to disable each attack selectively
    -x/-x0	Disable last keybytes brutforce
    -x1	Enable last keybyte bruteforcing (default)
    -x2	Enable last two keybytes bruteforcing
    -X	Disable bruteforce multithreading (SMP only)
    -s	Show the key in ASCII while cracking
    -y	Experimental single bruteforce attack which should only be used when the standard attack mode fails with more than one million IVs
    -z	Invokes the PTW WEP cracking method (Default in v1.x)
    -P	number	Long version --ptw-debug. Invokes the PTW debug mode: 1 Disable klein, 2 PTW.
    -K	Invokes the Korek WEP cracking method. (Default in v0.x)
    -D	Long version --wep-decloak. Run in WEP decloak mode
    -1	Long version --oneshot. Run only 1 try to crack key with PTW
    -M	number	(WEP cracking) Specify the maximum number of IVs to use
    -V	Long version --visual-inspection. Run in visual inspection mode (only with KoreK)
    
WEP and WPA-PSK cracking options

    -w	words	Path to a wordlists or “-” without the quotes for standard in (stdin). Separate multiple wordlists by comma
    -N	file	Create a new cracking session and save it to the specified file
    -R	file	Restore cracking session from the specified file
    
WPA-PSK options

    -E	file	Create EWSA Project file v3
    -j	file	Create Hashcat v3.6+ Capture file (HCCAPX)
    -J	file	Create Hashcat Capture file
    -S	WPA cracking speed test
    -Z	sec	WPA cracking speed test execution length in seconds
    -r	database	Utilizes a database generated by airolib-ng as input to determine the WPA key. Outputs an error message if aircrack-ng has not been compiled with sqlite support
    
SIMD Selection

    --simd	optimization	Use user-specified SIMD optimization instead of the fastest one
    --simd-list	Shows a list of the SIMD optimizations available
```

</details>





















