```plaintext
                                                     
  __ _  ___ _ __ ___  _   _        /\ /\/\   /\/\/\  
 / _` |/ _ \ '_ ` _ \| | | |_____ / //_/\ \ / /    \ 
| (_| |  __/ | | | | | |_| |_____/ __ \  \ V / /\/\ \
 \__, |\___|_| |_| |_|\__,_|     \/  \/   \_/\/    \/
    |_|   
  
[*] Adding bridge network to ethernet interface (with nmcli)                                        
```
# Instructions
1. Verify 'name' of your ethernet-card (Ex. enp1s0):
```bash
nmcli device
```
2. Create the bridge (Ex. br0):
```bash
nmcli con add type bridge con-name br0 ifname br0 stp yes
```
3. Add your ethernet-card to the bridge:
```bash
nmcli con add type ethernet slave-type bridge con-name newcon ifname enp1s0 master br0  
```
4. Finally activate the bridge:
```bash
nmcli con up br0
```
5. The connections look like:
```bash
$ nmcli con show

NAME                UUID                                  TYPE      DEVICE
br0                 4cc38959-a7ab-4e4b-a962-3a71b24f9b5c  bridge    br0
lo                  64d39acf-76fb-4ee8-a111-7efe0e13e538  loopback  lo
newcon              f0f44514-11bd-464e-9a94-9fdd35e260b6  ethernet  enp1s0
```
