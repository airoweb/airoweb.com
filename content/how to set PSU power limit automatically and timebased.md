+++
title = "How to change PSU power limit based on day/night automatically?"
date = 2020-03-18

[taxonomies] 
categories = ["Mining", "Braiins OS+"]
tags = ["bosminer", "cron"]
+++

In some countries there is electricity grid program and the electricity cost is different during a day, so if you want to power up your mining devices with low and hight PSU power limit in day/night you can follow the steps below.
  <!-- more -->

1. Login to the Braiins OS+ web interface and navigate to System > Schedule Tasks

2. Copy and paste the following command to the text area and save it.
```bash
0 9 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 1250/psu_power_limit = 900/' /etc/bosminer.toml && /etc/init.d/bosminer start
```
```bash
0 21 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 900/psu_power_limit = 1250/' /etc/bosminer.toml && /etc/init.d/bosminer start
```

4. If the scheduled task field was empty before this, SSH again to the device run the command below:
/etc/init.d/cron restart

5. Set device time zone to your proper time zone 

6. Happy mining!

> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!