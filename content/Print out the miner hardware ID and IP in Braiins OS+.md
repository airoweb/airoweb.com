+++
title = "Print out the miner hardware ID and IP in Braiins OS+"
date = 2021-08-01

[taxonomies] 
categories = ["Braiins OS+"]
+++

With the installed Braiins OS+, all devices get a uniq identifier ID called Hardware ID, in some case you need to find out the Hardware ID and the related IP. 
<!-- more -->

You can collect Hardware ID and IP in a logs.txt file through the command below in the Toolbox:

For 22.08 and higher:
```bash
bos-toolbox command -o -p root ip.csv "cat /tmp/miner_hwid | tr '\n' ' ' && cat /etc/network.conf | grep ipaddress"
```

For 22.05 and lower:
```bash
bos-toolbox command -o -p root ip.csv "cat /tmp/miner_hwid && uci show network.lan.ipaddr" > logs.txt
```