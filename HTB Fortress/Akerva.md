# Nmap
```bash

```

## Flag 1 Plain Sight
View source in the web application.

## Flag 2 Take a Look Around
```bash
snmpwalk -v 2c 10.13.37.11 -c public

[...SNIP...]
so.3.6.1.2.1.25.4.2.1.5.1230 = STRING: "-c /opt/check_devSite.sh"
iso.3.6.1.2.1.25.4.2.1.5.1231 = STRING: "/opt/check_backup.sh"
iso.3.6.1.2.1.25.4.2.1.5.1232 = STRING: "/opt/check_devSite.sh"
iso.3.6.1.2.1.25.4.2.1.5.1235 = STRING: "/var/www/html/scripts/backup_every_17minutes.sh AKERVA{IkN0w_SnMP@@@MIsconfigur@T!onS}"
iso.3.6.1.2.1.25.4.2.1.5.1236 = STRING: "/var/www/html/dev/space_dev.py"
iso.3.6.1.2.1.25.4.2.1.5.1241 = STRING: "/var/www/html/dev/space_dev.py"
iso.3.6.1.2.1.25.4.2.1.5.1243 = STRING: "--socket-activation"
[...SNIP...]
```
