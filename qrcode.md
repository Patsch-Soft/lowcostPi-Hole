#Small bash script for QR-Code in Terminal

```
#!/bin/bash
# nur qrcode anzeigen lassen
echo Zum Anzeigen des QR Code
echo nachfolgend den Benutzername
echo eingeben.
echo
read -p 'Wireguard Benutzer: ' wguser
echo
echo WG-User "$wguser.conf"
qrencode -t UTF8 < ~/"$wguser.conf"
```
