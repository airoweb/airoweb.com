+++
title = "Collect support logs through the SSH in Braiins OS+"
date = 2021-08-14

[taxonomies] 
categories = ["Braiins OS+"]
tags = ["bosminer", "ssh", "logs"]
+++

In some case the Quick Action > Get help doesn't work, so you can collect logs by the command below.

<!-- more -->

```ssh
ssh root@10.11.1.2 "/usr/sbin/support archive" && scp root@10.11.1.2:/tmp/support* ./
```

Use `scp` command will trannsfer data to your system.

> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!
