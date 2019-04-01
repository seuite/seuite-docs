# DDNS SetUp


A recommended way to simply update the host IP is through curl the NameCheap web API service scheduled. The URL is shown below:

[https://dynamicdns.park-your-domain.com/update?host=[host]&domain=[domain_name]&password=[ddns_password]&ip=[your_ip]](https://dynamicdns.park-your-domain.com/update?host=%5Bhost%5D&domain=%5Bdomain_name%5D&password=%5Bddns_password%5D&ip=%5Byour_ip%5D)

**Host** = @ (for example: wiki)

**Domain Name** = yourdomain.tld (for example: encofcomic.com)

**Dynamic DNS Password** = passwd

**IP Address** = optional value. If you don't specify any IP, the IP from which you are accessing this URL will be set for the domain.

## How to get local/intranet ip

ip=[`ifconfig |grep broadcast |awk '{print $2}'`] : use bash to pass intranet ip