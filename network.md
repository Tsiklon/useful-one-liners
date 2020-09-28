## Traffic capture + stats using iperf

### Server listening - tcp --
` iperf -s `

###  Server listening - udp --
` iperf -s -u `

###  Server sending - tcp --
` iperf -c <listening server ip> -t <max time> -i <update interval seconds> -w <tcp window size> `

### Server sending - udp --
` iperf -c 192.168.216.148 -u -b 100m -t 5 `

### All Traffic Between two hosts --- replace iface and ip's as appropriate
` tcpdump -n -i <iface> "host <host1-ip> and <host2-ip>" `

### All Traffic on a port on a host - writes pcap file ---
` tcpdump -n -i <interfacename> "dst host <hostip> and dst port <host port>" -w /path/to/output.pcap  `

### All Traffic between two hosts and a port
` tcpdump -n -i <interface> "(dst host <server 1 ip> or dst host <server 2 ip>) and (dst port <port> or src port <port>)" -w /path/to/output.pcap `

### All Multicast Traffic on a particular interface
` tcpdump -nn -i <interface> multicast and not broadcast `

### All Traffic on a particular interface going to a particular Multicast IP
` tcpdump -nn -i <interface> dst <MulticastIP> and multicast `
## Listening ports - udp and tcp ---
` netstat -tulpn `

## MAC Address list - DMESG ---
` dmesg | egrep -i "^eth.*\b(([a-f0-9]{2}:){5}[a-f0-9]{2}|[0-9a-f]{12})\b" | sed -r 's/([a-f0-9]{2})([a-f0-9]{2})([a-f0-9]{2})([a-f0-9]{2})([a-f0-9]{2})([a-f0-9]{2})/\1:\2:\3:\4:\5:\6/i'" `

## Check all IP's for a domain on a port ---
` for i in $(dig example.com |grep -A 100 "ANSWER SECTION"| grep -v ";;" | awk '{print $5}'| grep -v '^$'); do nc -vz $i 443; done `

## Port check (rhel6) --
` nc -vz <host ip> <port> `

## Port check (rhel7) --
` echo | nc -w1 {host ip} {port} >/dev/null 2>&1; echo $? ` 

## Port Check absent of netcat
` timeout 3 bash -c '</dev/tcp/{host}/{port}' && echo -e "Return code $? - Port open." || echo -e "Return code $? - Port Closed" `
