# LG Smart IP Camera Backup Download

```
#==========================================================================#
# Exploit Title: LG Smart IP Device Backup Download
# Date: 09-11-2018
# Exploit Author: Ege Balcı
# Vendor Homepage: https://www.lg.com
# Model: LNB*/LND*/LNU*/LNV*"
# CVE: ???"
#==========================================================================#
```

LG smart network camera devices are suffering from a broken access control vulnerability. Attackers are able to download certain log and backup files without authenticating into the system. Subject backup files contain user credentials and configuration information for the camera device. A malicious attacker is able to find the out the backup file name via reading the system logs, report data or just by brute-forcing the backup file name pattern.

[Known Affected Product List](https://github.com/egebalci/LG-Smart-IP-Device-Backup-Download/blob/master/affected_products.txt)

## POC

Following POC exploit bruteforces the backup file name and extracts the users.

![usage](https://github.com/egebalci/LG-Smart-IP-Device-Backup-Download/raw/master/Screenshot_4.png)

## Reproduce

Onces the target camera user clicks on the "View Report" button inside "Log & Report" page, the subject device generates a system report information file under  `/updownload/t.report`. This file can be downloaded directly witout authenticating to system.

![report](https://github.com/egebalci/LG-Smart-IP-Device-Backup-Download/raw/master/Screenshot_1.png)

This file contains information about the model ID and the version number of the target camera device. When the target camera user generates a system configuration backup by clicking the "Backup" button inside the mantenance page system uses the model ID, version number and the current date to name the backup file. With gathering those information by reading the report data or just by brute forcing the backup file name pattern with publicly known product information, attackers are able to download the backup files with using the `download.php?file=` endpoint.

![download](https://github.com/egebalci/LG-Smart-IP-Device-Backup-Download/raw/master/Screenshot_2.png)

Backup file is a compressed sqlite database system configuration informations can be extracted with using sqlite browsers.

![backup](https://github.com/egebalci/LG-Smart-IP-Device-Backup-Download/raw/master/Screenshot_3.png)

