# dynamic-ipsec-scripts

Scripts present in here should be helpful in a case, when you want to create VPN across two sites based on IPsec. Site-to-site IPsec requires on both endpoints public static IP adresses, which is more expensive than using dynamic IP addresses.

## Prerequisites

All sites, where will be VPN, require public IP. This is a limitation of IPsec protocol in site-to-site mode. If it's not possible to get public IP on either of your sites, try other VPN solution instead, e.g. [OpenVPN](https://openvpn.net/).

## How does it work
- Customer sets up IPsec tunnel across two sites. In configuration should be set endpoint IP addresses, which are assigned to routers at the moment.
- Customer sets up dynamic DNS service, which will create binding between dynamic IP address and domain. This way it is possible to reach the endpoints using their domain names. Good example of such service can be found [here](http://freedns.afraid.org/).
- Customer imports the scripts and schedules them to run periodically, e.g. once per 10 minutes.
 
## Platform support

At this moment, scripts are available for Mikrotik's RouterOS platform and were tested on latest version 6.x.x.

For details on how to use the scripts in [RouterOS](http://www.mikrotik.com/), see Readme file in the [mikrotik](/mikrotik) directory.
