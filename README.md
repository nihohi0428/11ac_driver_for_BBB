2014/08/29 Fr.

### Environment
- BeagleBoneBlack(BBB) Ubuntu 12.04
    - http://www.armhf.com/boards/beaglebone-black/#precise
- WLAN adaptor:ELECOM WDC-867U3

### How to install it
- Download 8812au.ko in this repository on your BBB.
- Put it on the following module directory.
```
$ sudo cp 8812au.ko /lib/modules/3.8.13-bone30/kernel/net/wireless/
$ sudo chmod 644 /lib/modules/3.8.13-bone30/kernel/net/wireless/8812au.ko 
$ sudo /sbin/depmod -a 3.8.13-bone30
```
### How to start it
- Insert your WLAN adaptor to your BBB.
- Load the driver.
```
$ sudo modprobe 8812au
```
- Configure your wlan setting.
```
$ cat /etc/wpa_supplicant.conf
network={
        ssid="Your AP"
        proto=WPA RSN   
        key_mgmt=WPA-PSK
        pairwise=CCMP
        group=CCMP
        psk="password"
        wpa_ptk_rekey=600
}
```
- You can check iwconfig command.
```
$ sudo iwconfig
wlan0     IEEE 802.11AC  ESSID:"Your AP"  Nickname:"xxxxx"
          Mode:Managed  Frequency:5.5 GHz  Access Point: aa:bb:cc:xx:yy:zz
          Bit Rate:867 Mb/s   Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Encryption key:****-****-****-****-****-****-****-****   Security mode:open
          Power Management:off
          Link Quality=100/100  Signal level=-45 dBm  Noise level=0 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

lo        no wireless extensions.

eth0      no wireless extensions.

rename4   unassociated  Nickname:"xxxxx"
          Mode:Managed  Frequency=2.412 GHz  Access Point: Not-Associated   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=0/100  Signal level=0 dBm  Noise level=0 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```
### How to build it
- See http://d.hatena.ne.jp/nihohi/