# Setup bind on ubuntu2204

Upgrade your system:
```bash
sudo apt update -y && sudo apt upgrade -y
```

Install bind server (bind utils for testing (e.g. dig or nslookup)):
```bash
sudo apt install bind9 bind9utils -y
```

Configure main bind config in `/etc/bind/named.conf.options`, and add something like this:
```bash
options {
    directory "/var/cache/bind";

    recursion yes;
    allow-query { any; };

    forwarders {
      1.1.1.1;
      8.8.8.8;
    };

    dnssec-validation auto;

    listen-on-v6 { any; };
};
```

Configure zones in `/etc/bind/named.conf.local`:
```bash
zone "example.com" {
    type master;
    file "/etc/bind/zones/db.example.com";
};

zone "0.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192.168.0";
};
```

Create forward zone in `/etc/bind/zones/db.example.com`:
```bash
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      ns1.example.com.
@       IN      A       192.168.0.1
ns1     IN      A       192.168.0.1
www     IN      A       192.168.0.1
```

Create reverse lookup zone in `/etc/bind/zones/db.192.168.0`:
```bash
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      ns1.example.com.
1       IN      PTR     example.com.
```


Check syntax:
```bash
sudo named-checkconf
sudo named-checkzone example.com /etc/bind/zones/db.example.com
sudo named-checkzone 0.168.192.in-addr.arpa /etc/bind/zones/db.192.168.0
```

Disable systemd resolver and add localhost to the resolv.conf:
```bash
sudo systemctl disable systemd-resolved.service
sudo systemctl stop systemd-resolved.service
sudo rm /etc/resolv.conf
sudo echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

Enable bind server:
```bash
sudo systemctl enable --now bind9
```

Allow dns traffic from outside (optional):
```bash
sudo ufw allow 53
```


Check stuff with bind utils (@localhost is the dns to query):
```bash
dig @localhost example.com
dig -x 192.168.0.1 @localhost
dig @localhost example.com A
dig @localhost example.com AAAA
dig @localhost example.com MX
dig @localhost example.com TXT
dig @localhost example.com CNAME
dig @localhost example.com NS
dig @localhost example.com SOA
```


Additionally you can install `webmin` to configure the bind dns via UI:
```bash
wget -q -O - http://www.webmin.com/jcameron-key.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://download.webmin.com/download/repository sarge contrib" > /etc/apt/sources.list.d/webmin.list'
sudo apt update
sudo apt install webmin
sudo systemctl enable --now webmin
sudo ufw allow 10000
```

Access the dashboard on `https://<your_server_ip>:10000`, and add the bind server in the "Servers" tab.