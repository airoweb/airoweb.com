+++
title = "Check pool status and restart BOSminer with Toolbox"
date = 2021-08-20

[taxonomies] 
categories = ["Braiins OS+"]
+++

The pool URLs in the Braiins OS+ and mostly all firmwares are failover for each other and if the first pool deads, the second one will work.
<!-- more -->
In some cases the farm has one URL and you need to check the machines for their Status and reload them.

Run the command to download the latest BOS+ Toolbox:
```
cd / && wget http://feeds.braiins-os.com/toolbox/latest/bos-toolbox && chmod+x ./bos-toolbox
```

Save the code below in a file "checkpool.sh" and save it in the beside of Toolbox.
```bash
#!/bin/bash

DIR=$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )
PASSWORD=root

if [[ $1 == "check" ]] || [[ $1 == "check_reload" ]]
then
  for i in {2..255}
  do
    ip="192.168.1.$i"
    fping -c1 -t100 $ip 2>/dev/null 1>/dev/null
    if [ "$?" = 0 ]
    then
      if ! echo '{"command":"version"}' | nc $ip 4028 |jq ."VERSION"[]."BOSminer"  | grep -q bosminer
      then
        echo "$ip no bosminer found"
      else
        pool_status=$(echo '{"command":"pools"}' | nc $ip 4028 | jq ."POOLS"[]."Status")
        if [[ $pool_status == 'Dead' ]]
        then
          echo "$ip : pool is $pool_status, Restart miner"
          if [[ $1 == "check_reload" ]]
          then
            "$DIR"/bos-toolbox command $ip -p $PASSWORD "/etc/bosminer.toml && /etc/init.d/bosminer restart"
          fi
        else
          echo "$ip : pool status is $pool_status"
        fi
      fi
    else
      echo "$ip OFFLINE"
    fi
  done
else
  echo "Ivalid Input, Use: check or check_reload"
fi
```

Give it the excutive permission:
```
chmod+x ./checkpool.sh
```

To set the cronjob on the linux machine open the terminal and type:
```
vi /etc/crontab
```

Copy nd paste the code below:
```
*/30 * * * * /checkpool
```

Please let me know if you find any issue. [@airoweb](https://t.me/airoweb)


> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!