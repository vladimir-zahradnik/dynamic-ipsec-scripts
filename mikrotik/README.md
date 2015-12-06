# Mikrotik scripts

Here are specific instruction to scripts created for RouterOS platform and were tested across two sites, both running RouterOS of the same version.

## Prerequisites

- Configure site-to-site IPsec tunnel across both sites. Public IP is a must for both endpoints. This [webpage](http://wiki.mikrotik.com/wiki/Manual:IP/IPsec) is a good place to start. I've been using IPsec in ESP tunnel mode, but other modes should in theory work just fine.
- Set up account on dynamic DNS service provider. The scripts use [freedns.afraid.org](http://freedns.afraid.org/), but other services should work as well. You will just need to modify the scripts to work with different DNS service (make sure they have public API available).

## Description of scripts

The scripts want to access specified interfaces or rules directly on the router. Interfaces are matched using _interface-name_, but rules are represented on router just as entries with number. To identify the specific rule with highest confidence, script finds the match using comment on the rule. Therefore make sure the rules and interfaces have proper comment and put this exact comment into scripts.

### mikrotik_dns_update.script

This script tracks assigned IP address on WAN interface of the router. It assumes that the interface has assigned public IP address directly from your ISP. If the ISP assigns new IP address, on next scheduled run will the script update the dynamic DNS service. This script makes the assigned IP available as a global variable available to the whole system and other scripts.

### mikrotik_ipsec_update.script

This script tracks for changes of locally asigned IP address as well as IP change on remote IPsec endpoint. In either cases it will update IPsec policies, peer information and firewall rules.

### mikrotik_ovpn_update.script

This script is not needed in pure IPsec setup. However it may be useful in cases, where there is another VPN on endpoint with dynamic IP. It is running on a client router and is tracking for endpoint IP changes.

## Setup

- Before you import the scripts, you should review them and modify to suit your needs. Albeit they are quite generic, some information should be updated. Put there your credentials to dynamic DNS service, domain names and DNS entry name for your sites. You should also configure, which router rules should be updated. You can find commented examples in the scripts.
- Import the scripts and configure Scheduler to run them periodically. Alternative is to set up a trigger which tracks reachability of given IP.
