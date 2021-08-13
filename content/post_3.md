+++
title = "How to change PSU power limit based on day/night automatically?"
date = 2020-03-18

[taxonomies] 
categories = ["Mining", "Braiins OS+"]
tags = ["bosminer", "cron"]
+++

You should follow these steps:


1. Login to the Braiins OS+ web interface and navigate to System > Schedule Tasks

2. Copy and paste the following command to the text area and save it.
```bash
0 9 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 1250/psu_power_limit = 900/' /etc/bosminer.toml && cp /etc/tune900.json /etc/bosminer-autotune.json && /etc/init.d/bosminer start
```
```bash
0 21 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 900/psu_power_limit = 1250/' /etc/bosminer.toml && cp /etc/tune1250.json /etc/bosminer-autotune.json && /etc/init.d/bosminer start
```

3. If the scheduled task field was empty before this, SSH again to the device run the command below:
/etc/init.d/cron restart

4. Set device time zone to your proper time zone 

5. Happy mining!