# IP Address:
* An IP address is a unique address that identifies a device on the internet or a local network. IP stands for "Internet Protocol," which is the set of rules governing the format of data sent via the internet or local network.
* IP address has four octets as shown below :
```
00000000    .  00000000      .  00000000      .  00000000
(2^8)-1=255 .  (2^8)-1=255   .  (2^8)-1=255   .  (2^8)-1=255
0-255       .  0-255         .  0-255         .  0-255

10          .  0             .  0             .  0
00001010    .  00000000      .  00000000      .00000000
```
* Binary-Decimal/Decimal-Binary calculator -- [REFERHERE](https://www.calculator.net/binary-calculator.html)

### Private/Public IP Ranges :
```
| Private IP's Range:           | Public Ip's Range:                             |
| ----------------------------- | ---------------------------------------------- |
| 10.0.0.0 – 10.255.255.255,    | Besides private IP addresses, rest are public. |
| 172.16.0.0 – 172.31.255.255,  |                                                |
| 192.168.0.0 – 192.168.255.255 |                                                |
```

# CIDR 
* Classless Inter-Domain Routing (CIDR) is a range of IP addresses a network uses. A CIDR address looks like a normal IP address, except that it ends with a slash followed by a number. The number after the slash represents the number of addresses in the range.

### CIDR Understanding:
* Example : 10.0.0.0/24  --> 2^32-24 = 2^8 = 256 Ip's
* CIDR calculator [REFERHERE](https://account.arin.net/public/cidrCalculator)
![preview](../images/CIDR1.png)

```
| IPv4 CIDR IP/CIDR | Number_Of_Ip's(2^32-n) |
| ----------------- | ------------------------ |
| a.b.c.d/32        | 1                        |
| a.b.c.d/31        | 2                        |
| a.b.c.d/30        | 4                        |
| a.b.c.d/29        | 8                        |
| a.b.c.d/28        | 16                       |
| a.b.c.d/27        | 32                       |
| a.b.c.d/26        | 64                       |
| a.b.c.d/25        | 128                      |
| a.b.c.0/24        | 256                      |
| a.b.c.0/23        | 512                      |
| a.b.c.0/22        | 1,024                    |
| a.b.c.0/21        | 2,048                    |
| a.b.c.0/20        | 4,096                    |
| a.b.c.0/19        | 8,192                    |
| a.b.c.0/18        | 16,384                   |
| a.b.c.0/17        | 32,768                   |
| a.b.0.0/16        | 65,536                   |
| a.b.0.0/15        | 1,31,072                 |
| a.b.0.0/14        | 2,62,144                 |
| a.b.0.0/13        | 5,24,288                 |
| a.b.0.0/12        | 10,48,576                |
| a.b.0.0/11        | 20,97,152                |
| a.b.0.0/10        | 41,94,304                |
| a.b.0.0/9         | 83,88,608                |
| a.0.0.0/8         | 1,67,77,216              |
| a.0.0.0/7         | 3,35,54,432              |
| a.0.0.0/6         | 6,71,08,864              |
| a.0.0.0/5         | 13,42,17,728             |
| a.0.0.0/4         | 26,84,35,456             |
| a.0.0.0/3         | 53,68,70,912             |
| a.0.0.0/2         | 1,07,37,41,824           |
| a.0.0.0/1         | 2,14,74,83,648           |
| 0.0.0.0/0         | 4,29,49,67,296           |
```







