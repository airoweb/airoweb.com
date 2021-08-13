+++
title = "How to call BOSminer API in Python?"
date = 2021-07-18

[taxonomies] 
categories = ["Braiins OS+"]
tags = ["bosminer", "api", "python"]
+++



```python
#!/usr/bin/python3
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("10.10.1.2", 4028))
s.send(b'{"command":"pools"}\n')
data = s.recv(2048)
s.close()
print(data.decode("ascii"))
```

> Get [Braiins OS+](https://braiins-os.com?utm_source=airoweb) to increase your mining devices efficiency!