+++
title = "Configuring Braiins OS+ Firmware: Harnessing the Power of Braiins Toolbox 23.12"
date = 2023-12-26

[taxonomies] 
categories = ["Braiins Toolbox", "Braiins OS+", "ASIC Miners", "Mining Firmware"]
+++

Unlocking new possibilities with the recent release of Braiins Toolbox 23.12, users can now seamlessly configure their ASIC miners during the Braiins OS+ installation process. This revolutionary feature 
<!-- more -->

eliminates the need for additional steps, allowing both large-scale mining farms and their tech enthusiasts to streamline daily operations and save valuable time.

```bash
./braiins-toolbox firmware install --url stratum2+tcp://3ehzad.{{miner.mac}}@v2.eu.stratum.braiins.com/u95GEReVMjK6k5YqiSFNqqTnKU4ypU2Wm8awa6tmbmDmk1bWt
 --url stratum+tcp://3ehzad.{{miner.ip}}@eu.stratum.braiins.com:3333 --power 2000 --dps on --shutdown-enabled true --shutdown-duration 3 --cooling-mode standard -i iplist.txt
```

Another notable enhancement empowers farm operators to set workernames effortlessly by utilizing the miner's MAC address, IP, and Hostname in the pool settings via Braiins Toolbox, doable on GUI or CLI mode.

For a detailed overview of the latest changes in version 23.12, check out the [changelog](https://feeds.braiins-os.com/braiins-toolbox/#5a4c12bc-0000-4d0b-a167-e07acee5e131?utm_source=airoweb).

Ready to optimize your mining experience? Download the [Braiins Toolbox](https://braiins.com/toolbox#download?utm_source=airoweb) now and seamlessly install Braiins OS+ on your S19 Antminers!
