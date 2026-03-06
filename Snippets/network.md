# network

## Find Devices with Open Port in Subnet

`network` `scan` `port` `subnet`  Scans a /24 subnet to find IP addresses with a specific port (default 80) open. Adjust the base IP and port as needed.


---

### bash

```bash
for ip in 192.168.1.{1..254}; do nc -z -w 1 $ip 80 2>/dev/null && echo "$ip:80 is open"; done
```

### pwsh

```powershell
1..254 | ForEach-Object -Parallel { $ip="192.168.1.$_"; if(Test-NetConnection $ip -Port 80 -WarningAction SilentlyContinue | Where-Object TcpTestSucceeded) { Write-Output "$ip:80 is open" } } -ThrottleLimit 50
```

## Discover Local mDNS Services

`mdns` `zeroconf` `discovery` `network` **Description:** Scans the local network for advertised mDNS/Zeroconf services. Perfect for finding IoT devices or local web servers.


---

### bash

```bash
avahi-browse -a -r -t
```

### pwsh

```powershell
Resolve-DnsName -Name _services._dns-sd._udp.local -Type PTR
```

## Resolve Hostname from IP (Reverse DNS)

`dns` `hostname` `nslookup` `resolve` Performs a reverse DNS lookup to find the hostname associated with a specific IP address.


---

### bash

```bash
dig +short -x 8.8.8.8
```

### pwsh

```powershell
Resolve-DnsName -Name 8.8.8.8 | Select-Object -ExpandProperty NameHost
```

### cmd

```powershell
nslookup 8.8.8.8
```

## SSH Local Port Forwarding

`ssh` `port-forward` `tunnel` `mapper` Forwards a local port to a remote destination through an SSH tunnel (e.g., securely access a remote database or web UI). Works across all modern terminals since OpenSSH is native everywhere now.


---

### bash

```bash
ssh -L 8080:localhost:80 user@remote-server -N
```

## Show Listening Ports and PIDs

`ports` `listen` `troubleshooting` `pid` Lists all actively listening ports on your local machine and the Process IDs bound to them so you know what is hogging a port.


---

### bash

```bash
sudo ss -tulpn | grep LISTEN
```

### pwsh

```powershell
Get-NetTCPConnection -State Listen | Select-Object LocalAddress, LocalPort, OwningProcess
```

cmd

```powershell
netstat -ano | findstr LISTENING
```

## Get Public IP Address

`ip` `public` `wan` `curl` Quickly fetches your router's external public IP address using a free API.


---

### bash

```bash
curl -s ifconfig.me
```

### pwsh

```bash
(Invoke-RestMethod -Uri "https://ifconfig.me").Trim()
```

### cmd

```powershell
curl -s ifconfig.me
```