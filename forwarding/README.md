## Create Private DNS Zone with forwarding
Note: 10.128.0.46 is the DNS server node (vm)
![private dns zone](./img/private_dns_zone.png)



## Create DNS Server on Ubuntu 18.04 LTS
```
sudo apt update
sudo apt upgrade

sudo apt install bind9 bind9utils bind9-doc dnsutils
```

```
sudo nano /etc/bind/named.conf.local
```
Enter the following content:
```
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone    "glau.private"   {
        type master;
        file    "/etc/bind/forward.glau.private";
 };
```

```
sudo nano /etc/bind/forward.example.com
```
Enter the following content:
```
$TTL 1d
@               IN      SOA     dns1.glau.private.    hostmaster.glau.private. (
                1        ; serial
                6h       ; refresh after 6 hours
                1h       ; retry after 1 hour
                1w       ; expire after 1 week
                1d )     ; minimum TTL of 1 day
;
;
;Name Server Information 
@               IN      NS      ns1.glau.private.
ns1             IN      A       10.128.0.46
;
;
glau2-vm        IN      A       10.128.0.49
glau3-vm        IN      A       10.128.0.53
```



