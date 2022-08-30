## Ping Verification Script

When adding a new device to the internal network, I want to make sure all devices in that network can see each other. Basically, when I add an IP to the internal network, which is usually to add a system, I want to make sure that system can detect all other devices in that system.

**#!/usr/bin/python**

- The plan is to run a loop of trying to ping each IP in the subnet 192.168.50.0/24. Want to make sure it runs a full loop to 254 to make sure there’s not an IP that’s being used that shouldn’t be in use. Also, make a script for only running hosts to be pinged.
    - **for i in range (254):**
    - **n = 0**
        - **while n ≤ 254:**
        - **n+=1**
    - **ip_list = ’192.168.50.’ + n**
- We’ll want to import the os as we’ll be using ping.
    - **import os**
    - **response = os.popen(ping, ip_list).read()**
- Ping received response: “64 bytes from”
    - **if “64 bytes from” in response:**
        - **print(”{ip} up, host reachable.”)**
- Unreachable response: “Request timeout”
    - **else:**
        - **print(”{ip} down, host unreachable.”)**

## Full Verification Script

```python
import os

host = 0
while host <= 254:
    ip = '192.168.50.' + str(host)
    response = os.popen('ping ' + (ip) + ' -c1').read()
    if "64 bytes from" in response:
        print((ip) + " up, host reachable.")
    else: 
        print((ip) + " down, host unreachable.")
    host= host + 1
```

## Running Hosts Verification Script

```python
import os

host = 0
while host <= 20:
    ip = '192.168.50.' + str(host)
    response = os.popen('ping ' + (ip) + ' -c1').read()
    if "64 bytes from" in response:
        print((ip) + " up, host reachable.")
    else: 
        print((ip) + " down, host unreachable.")
    host= host + 1
```
I'm not too familiar with the popen module so I had to play around with the formatting of the ping. Overall, this was very simple. 

## Helpful Resources
- [https://docs.python.org/3/library/os.html#os.popen](https://docs.python.org/3/library/os.html#os.popen)
