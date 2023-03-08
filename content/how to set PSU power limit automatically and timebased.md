+++
title = "How to change Power Target/Limit based on day/night automatically on Braiins OS+?"
date = 2023-03-09

[taxonomies] 
categories = ["Mining", "Braiins OS+"]
+++

In some countries there is electricity grid program and the electricity cost is different during a day, so if you want to power up your mining devices with low and hight PSU power limit in day/night you can follow the steps below.
  <!-- more -->

> Note: This option is not available for Beaglebone and Amlogic control boards.

Login to the Braiins OS+ web interface and navigate to System > Schedule Tasks

Copy and paste the following command to the text area and save it.

For Braiins OS+ 22.08 and higher:
```bash
0 9 * * * /etc/init.d/bosminer stop && sed -i 's/^power_target = .*/power_target = 960/' /etc/bosminer.toml && /etc/init.d/bosminer start
```

```bash
0 9 * * * /etc/init.d/bosminer stop && sed -i 's/^power_target = .*/power_target = 1280/' /etc/bosminer.toml && /etc/init.d/bosminer start
```

For Braiins OS+ 22.05 and lower:
```bash
0 9 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 1250/psu_power_limit = 960/' /etc/bosminer.toml && /etc/init.d/bosminer start
```

```bash
0 21 * * * /etc/init.d/bosminer stop && sed -i 's/psu_power_limit = 900/psu_power_limit = 1280/' /etc/bosminer.toml && /etc/init.d/bosminer start
```


If the scheduled task field was empty before this, SSH again to the device run the command below:
/etc/init.d/cron restart

Set device time zone to your proper time zone 

Happy mining!


> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!