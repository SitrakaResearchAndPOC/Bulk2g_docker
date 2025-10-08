
docker build -t bulk2g_usrp -f Dockerfile.bulk2g_usrp .

docker rm -f bulk2g_usrp

 docker run -tid --privileged --cgroupns=host --net=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw -v /dev:/dev -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --tmpfs /run --tmpfs /run/lock --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bulk2g_usrp --hostname bulk2g_usrp bulk2g_usrp


docker exec -it bulk2g_usrp bash



docker exec -it bulk2g_usrp uhd_usrp_probe

docker exec -it bulk2g_usrp uhd_find_devices 

docker exec -it bulk2g_usrp osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg


ctrl+shift+t
docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/main_uhd_spoof.py

Testing USRP SpoofScript1 :

docker exec -it bulk2g_usrp bash osmo-nitb-scripts/scripts_spoof1/finding_imsi_extenstion.sh

docker exec -it bulk2g_usrp bash osmo-nitb-scripts/scripts_spoof1/set_imsi_extension.sh <IMSI> 0341220590


docker exec -it bulk2g_usrp  bash osmo-nitb-scripts/scripts_spoof1/finding_imsi_extenstion.sh

docker exec -it bulk2g_usrp  python2 osmo-nitb-scripts/scripts_spoof1/sending_sms_spoof_byextension.py

docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof1/sending_sms_broadcast.py 



Testing USRP SpoofScript2 : 
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/show_subscribers.py



Problème : 
docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/sms_spam.py <EXTENSION> 3 "link gmail"

Plus debug : 
docker exec -it bulk2g_usrp telnet 127.0.0.1 4242

docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/show_subscribers.py 

docker exec -it bulk2g_usrp python2 osmo-nitb-scripts/scripts_spoof2/sms_broadcast.py 165 "link gmail"




Testing USRP Fake SMS Sender:
RESTART ALL : 
docker exec -it bulk2g_usrp  osmo-trx-uhd -C /etc/osmocom/osmo-trx-uhd.cfg

docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/main_uhd.py


docker exec -it bulk2g_usrp python3 osmo-nitb-scripts/interact.py





DOCKER COMPOSE NOT RUN
 
docker-compose -f docker-compose.bulk2g_usrp.yaml   up -d 

docker-compose ps

docker-compose exec bulk2g_usrp

docker compose exec bulk2g_usrp uhd_usrp_probe

docker-compose exec bulk2g_usrp uhd_usrp_probe

xhost +; docker-compose exec bionicmodulation gnuradio-companion


