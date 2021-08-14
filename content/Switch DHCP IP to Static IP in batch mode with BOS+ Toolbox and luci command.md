+++
title = "Switch DHCP to Static IP in batch with BOS+ Toolbox and luci command"
date = 2021-06-23

[taxonomies] 
categories = ["Braiins OS+"]
tags = ["luci", "BOS+ Toolbox"]
+++

In some case we need to chamge DHCP IP to Static IP in our network, the idea is we get the currenct miners IP and set it to the device as a static IP in Braiins OS+.
<!-- more -->

First you should download the BOS+ Toolbox [[Windows Version](https://feeds.braiins-os.com/toolbox/latest/bos-toolbox.zip)] | [[Linux Version](https://feeds.braiins-os.com/toolbox/latest/bos-toolbox)]

Now you can run the command below:
```bash
./bos-toolbox command iplist.txt '. /lib/functions/network.sh; network_flush_cache; network_find_wan NET_IF; network_get_ipaddr NET_ADDR "${NET_IF}"; network_get_gateway NET_GW "${NET_IF}"; uci set network.lan.ipaddr=${NET_ADDR}; uci set network.lan.gateway=${NET_GW}; uci set network.lan.netmask="255.255.255.0"; uci set network.lan.proto="static"; uci commit network'
```

> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!