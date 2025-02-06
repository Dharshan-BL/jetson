
# Insturctions to hook-up Jetson(Or any PC) to a Host-PC over ethernet port

## 1. Setting up static IPs
Ensure that the IPs that you want to set has the same subnets: `192.168.7.x` and `192.168.7.y` (If you want to set it to different IPs, you need to do it over a router). I prefer to use netplan.

- Open the netplan on your `Host-PC`
```
sudo nano /etc/netplan/50-cloud-init.yaml
```
- Paste the following netplan in it and save
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.7.101/24
      gateway4: 192.168.7.101
      nameservers:
        addresses:
          - 8.8.8.8
```
- Open the netplan on your `Jetson`
```
sudo nano /etc/netplan/50-cloud-init.yaml
```
- Paste the following netplan in it and save
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.7.1/24
      gateway4: 192.168.7.101
      nameservers:
        addresses:
          - 192.168.7.101
          - 8.8.8.8
```

## 2. IP forwarding on `Host-PC`
- Enable IP forwarding:
  ```
  echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
  ```
## 3. Check iptables configuration on `Host-PC`
- Find the interface with internet and the interface that it should be forwarded to using:
  ```
  ip a
  ```
  (in my case it is from wlan0 to eth0)
- Apply the NAT rules:
  ```
  sudo iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
  sudo iptables -A FORWARD -i wlan0 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
  sudo iptables -A FORWARD -i eth0 -o wlan0 -j ACCEPT
  ```
- (optional) to keep it persistent save it using:
  ```
  sudo netfilter-persistent save
  sudo netfilter-persistent reload
  ```

## 4. Check internet connectivity on `Jetson`
```
ping -c 4 ubuntu.com
```
If you are unable to ping it, try pinging the DNS `8.8.8.8`. If that works, check your DNS settings again! 
