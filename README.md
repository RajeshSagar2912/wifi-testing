# --> Wifi-Pentesting
This repo will contains all my wifi pentesting useful concepts and commands. Here are the various kinds of attacks that can be performed while doing wifi pentesting: https://github.com/D3Ext/WEF/wiki/Attacks 

# --> Basic Concepts

## 1) SSID: Service Set Identifier

name of the Wi-Fi network you see when you open your phone or laptop.
When you check available Wi-Fi, you might see names like `Guest`, `HomeWiFi`, or `SchoolNet`.
--> in my case: the SSID is "Guest" — that’s the network name.

## 2) BSSID: Basic Service Set Identifier

It’s basically the unique ID of each Wi-Fi router or access point that broadcasts the SSID.
It looks like a series of numbers and letters (MAC address), e.g., b8:fe:90:31:13:8e.

## Example:

Imagine your school has a Wi-Fi network called "SchoolNet" (SSID).
There are multiple routers placed in different classrooms and hallways.
Each router has its own BSSID (like 74:88:bb:80:2c:a1 or 20:f1:20:ba:9b:c1).
When you connect to "SchoolNet", your device automatically chooses the router (BSSID) with the strongest signal near you.

So:
SSID = Wi-Fi network name (SchoolNet)
BSSID = Unique router ID (like classroom router #1, #2, etc.)

## 3) EAPOL: Extensible Authentication Protocol over LAN

It’s a protocol used in WPA/WPA2 authentication between a client (station) and an access point (AP).
When a device connects to Wi‑Fi, the AP and client exchange EAPOL packets to prove they both know the secret key (PSK or enterprise credentials).
If you capture those EAPOL packets, you can test whether the pre‑shared key (PSK) is weak.
Tools like aircrack-ng use the handshake to verify guesses from a wordlist against the real key.
Without EAPOL packets, you can’t crack WPA2‑PSK — that’s why your earlier attempt failed.

## 4) PSK: Pre‑Shared Key

It’s the most common Wi‑Fi authentication method for home and small business networks.
Everyone connects using the same password (the “Wi‑Fi key”).
Example: when you join a Wi‑Fi and type in a password like guest123, that’s PSK

## IMP NOTE:

### WPA2‑PSK networks → handshake cracking is possible.
### WPA2‑Enterprise networks (eduroam, ISB‑PGP, ISB‑WIFI, ISB‑YL) → they use username/password with RADIUS. You’ll still see EAPOL, but it’s not a PSK you can brute force with rockyou.txt. Testing here is about certificate validation and weak EAP methods, not handshake cracking.
