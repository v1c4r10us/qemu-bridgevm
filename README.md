```plaintext
                                                     
  __ _  ___ _ __ ___  _   _        /\ /\/\   /\/\/\  
 / _` |/ _ \ '_ ` _ \| | | |_____ / //_/\ \ / /    \ 
| (_| |  __/ | | | | | |_| |_____/ __ \  \ V / /\/\ \
 \__, |\___|_| |_| |_|\__,_|     \/  \/   \_/\/    \/
    |_|   
  
[*] Adding bridge network to ethernet interface (with nmcli)                                        
```
# Instructions
1. Verify 'name' of your interface card (Ex. eno1):
```bash
$ nmcli device
```
2. Delete actual ethernet connection:
```bash
$ nmcli con del eno1
```

3. Create the bridge (Ex. br0):
```bash
$ nmcli con add type bridge autoconnect yes con-name br0 ifname br0
```

4. Add ethernet slave connection:
```bash
$ nmcli con add type ethernet slave-type bridge con-name eno1 ifname eno1 master br0 
```


4. Modify the connection (Assign static IP if necesary)
```bash
$ nmcli con edit br0
nmcli> set ipv4.method manual
nmcli> set ipv4.address 172.15.5.254/24
nmcli> set ipv4.gateway 172.15.5.1
nmcli> set ipv4.dns 8.8.8.8
nmcli> save
nmcli> quit
```
5. Reboot the system
