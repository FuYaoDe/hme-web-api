ap_mode:
	ifdown wlan0
	sh hostapd.conf_create.sh
	cp hostapd.conf /etc/hostapd/hostapd.conf

	cp interfaces_ap /etc/network/interfaces
	cp hostapd /etc/default/hostapd
	cp udhcpd_ap /etc/default/udhcpd
	service hostapd start
	service udhcpd start
	ifup wlan0
	update-rc.d hostapd defaults
	update-rc.d udhcpd defaults

client_mode:
	service hostapd stop
	service udhcpd stop
	ifdown wlan0
	- rm /etc/default/hostapd
	cp udhcpd_client /etc/default/udhcpd

	sh wpa_supplicant.conf_create.sh
	cp wpa_supplicant.conf /etc/wpa_supplicant/wpa_supplicant.conf
	cp interfaces_client /etc/network/interfaces

	/etc/init.d/networking restart
	ifup wlan0
	update-rc.d -f hostapd remove
	update-rc.d -f udhcpd remove
