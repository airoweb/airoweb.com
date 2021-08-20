
+++
title = "Check pool status and restart BOSminer with Toolbox"
date = 2021-08-20

[taxonomies] 
categories = ["Braiins OS+"]
tags = ["BOS+ Toolbox", "Automation"]
+++

<!-- more -->


```bash
#!/bin/bash

DIR=$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )
PASSWORD=xxxxxx

if [[ $1 == "check" ]] || [[ $1 == "check_reload" ]]
then
  for i in {20..101}
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