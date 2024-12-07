# OpenWRT/Tailscale on Raspberry Pi 4
OpenWRT version 23.05
Raspberry Pi 4

see [this OpenWRT wiki page](https://openwrt.org/docs/guide-user/services/vpn/tailscale/start) for the basic setup guide
see [this OpenWRT wiki page](https://openwrt.org/toh/raspberry_pi_foundation/raspberry_pi) for all things Raspberry Pi
 
## Install Packages
#### 

```
opkg update
opkg install tailscale
opkg install iptables-nft kmod-ipt-conntrack kmod-ipt-conntrack-extra kmod-ipt-conntrack-label kmod-nft-nat 
opkg kmod-ipt-nat

```

## Enable Case Fan
see [here](https://openwrt.org/toh/raspberry_pi_foundation/raspberry_pi#adding_a_case_fan)

```
opkg update
opkg install kmod-hwmon-gpiofan
```

``` title="/boot/config.txt"
# temperature in milliCelsius
dtoverlay=gpio-fan,gpiopin=14,temp=80000
```

## Configure networks
#### LAN network configuration
``` title="/etc/config/network"
config interface 'lan'
        option device 'br-lan'
        option proto 'static'
        option ipaddr '192.168.10.1'
        option netmask '255.255.255.0'
        option ip6assign '60'
        list dns '1.1.1.1'
        list dns '8.8.8.8'
```
#### Tailscale interface
```
config interface tailscale
	option device 'tailscale0'
	option proto 'none'
```

## Configure Wireless WAN (for Raspberry Pi 4)
``` title="/etc/config/wireless
config wifi-device 'radio0'
        option type 'mac80211'
        option path 'platform/soc/fe300000.mmcnr/mmc_host/mmc1/mmc1:0001/mmc1:0001:1'
        option channel '7'
        option band '5g'
        option htmode 'HT20'
        option hwmode '11g'
        option short_gi_40 '0'
        option disabled '0'

config wifi-iface 'wifinet1'
        option device 'radio0'
        option mode 'sta'
        option network 'wwan'
        option ssid 'Lothlorien'
        option encryption 'psk2'
        option key 'EnChus81222'
```

## Configure firewall rules for tailscale
#### Add a new zone
``` title="/etc/config/firewall"
config zone
	option name 'tailscale
	list network 'tailscale'
	option input 'ACCEPT'
	option output 'ACCEPT'
	option forward 'ACCEPT'
	option masq '1'
	option mtu_fix '1'
	
config forwarding 
	option src 'tailscale'
	option dest 'lan'

# At the end of the file
config rule
	option name 'Allow Tailscale UDP'
	option src '*'
	option target 'ACCEPT'
	option proto 'udp'
	option dest_port '41641'
	
config forwarding
	option src 'lan'
	option dest 'tailscale'

```