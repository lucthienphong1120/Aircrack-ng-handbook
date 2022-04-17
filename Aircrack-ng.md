# [Aircrack-ng](https://www.aircrack-ng.org/)

> Currently only vietsub version is available
> 
> Hiện mới chỉ có bản vietsub

## Sơ lược

Aircrack-ng là bộ công cụ dùng để pentest mạng không dây, crack wep và dò khóa wpa/wpa2-psk.

Aircrack-ng có rất nhiều công cụ, một số là:

### [Airmon-ng](https://www.aircrack-ng.org/doku.php?id=airmon-ng)

Enable monitor mode, kill network managers, go back managed mode, show the interfaces status

```
airmon-ng <start|stop> <interface> [channel] or airmon-ng <check|check kill>
```

### [Airodump-ng](https://www.aircrack-ng.org/doku.php?id=airodump-ng)

Detected access points, packet capture, capturing raw 802.11 frames, collecting WEP IVs or WPA handshakes, log the coordinates

```
airodump-ng <options> <interface>[,<interface>,...]

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

### [Aireplay-ng](https://www.aircrack-ng.org/doku.php?id=aireplay-ng)

Generate traffic, fake authentications, Interactive packet replay, hand-crafted ARP request injection and ARP-request reinjection


















