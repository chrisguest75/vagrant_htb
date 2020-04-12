# README.md
Build an ubuntu hack the box 
  
## Prequisites
[Vagrant Setup](../README.md)

## Build the VM

### Configure Network
Avoid adding to home network to prevent bridging. 

### Data Folder
1. Create a data folder in the repo root.
1. Download the ovpn file from HTB and copy to data folder

### Connect to HTB VPN
```sh
sudo openvpn /vagrant_data/<user>.ovpn

# why this??
sudo /usr/sbin/openvpn /vagrant_data/<user>.ovpn
```

### Test 
```sh
nmap -sV 10.10.10.0/24
smbclient -N -L \\\\10.10.10.27\\
smbclient -N  \\\\10.10.10.27\\backups
dir
get prod.dtsConfig
cat prod.dtsConfig
git clone https://github.com/SecureAuthCorp/impacket
pip install .
./mssqlclient.py ARCHETYPE/sql_svc@10.10.10.27 -windows-auth
```
