# Setting up ZTP for Cat9k

## Prereqs 

- DHCP Server (only 1 DHCP in the network)
- HTTP Server - nginx 
- Cat9k device with management port access to servers and 16.
- 


## nginx HTTP server configuration

### Install nginx on Ubuntu Server
```
$ sudo apt update
$ sudo apt install nginx
```
- open browser and enter http server IP address or localhost to verify 

### Add python script to /var/www/html directory

```
$ cd /var/www/html
$ touch ztp.py
$ sudo vim ztp.py
```

### Python Script Example


<img width="570" alt="python-script" src="https://user-images.githubusercontent.com/9085386/195929947-8938bc53-c2fd-4ff9-9459-26bcdda582aa.PNG">


## DHCP server configuration

### Install DHCP on Ubuntu Server
```
$ sudo apt update
$ sudo apt install isc-dhcp-server
```
### Access the /etc/dhcp/dhcpd.conf file with your IDE of choice

```
$ sudo vim /etc/dhcp/dhcpd.conf
```

### Enter the configuration to match your network environment

```
host <hostname> {
  hardware ethernet xx:xx:xx:xx:xx:xx;
  option dhcp-client-identifier "xxxxxxxxxxxxxx";
  option host-name "<hostname>".
  option log-servers x.x.x.x;
  fixed-address x.x.x.x;
  if option vendor-class-identifier = "..." {
    option vendor-class-identifier "...";
    if exists user-class and option user-class = "iPXE" {
      filename "http://x.x.x.x/…/<image>";
    } else {
      filename "http://x.x.x.x/…/<script-name>";
    }
  }
}

```
