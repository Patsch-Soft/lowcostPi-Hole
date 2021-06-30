Einfaches Script um die IP Adressen für PiHole anzupassen wenn die IP Adresse per DHCP bezogen wird. Die Datei befindet sich normalerweise in:

/etc/pihole/setupVars.conf


```
#!/bin/sh
#
# Einfaches Script zum Anpassen der setupVars.conf Datei
# wenn die IP-Adressen per DHCP zugewiesen wurde
#
ip4=$(/sbin/ip -o -4 addr list eth0 | awk '{print $4}' | head -n 1)
ip6=$(ip -6 addr show dev eth0 | awk '/inet6/{print $2}')
ip2="IPV4_ADDRESS="
ip3="IPV6_ADDRESS="

/etc/init.d/pihole-FTL stop
wait 5
# IPV Einträge löschen und .backup erstellen
sed '/^IPV/d' /etc/pihole/setupVars.conf > /etc/pihole/setupVars.backup
# setupVars.conf löschen und Datei ohne IPV Einträge kopieren
rm /etc/pihole/setupVars.conf
cp /etc/pihole/setupVars.backup /etc/pihole/setupVars.conf
rm /etc/pihole/setupVars.backup
# die mit ip ausgelesenen IP-Adressen einfügen
printf "$ip2$ip4"  >> /etc/pihole/setupVars.conf
printf "\n"  >> /etc/pihole/setupVars.conf
printf "$ip3$ip6"  >> /etc/pihole/setupVars.conf
printf "\n"  >> /etc/pihole/setupVars.conf

/etc/init.d/pihole-FTL start
```
