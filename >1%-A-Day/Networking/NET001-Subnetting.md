---
ID: NET001
Date: 26/06/2025
Tags: #Subnetting #Networking #IPv4
Category: Networking
---

# NET001 – Subnetting
 **Learned**
My current understanding about subnetting has been slowly desinagrated since I have learnt it in university, because of the fact I dont practice it. But it's a key foundation for learning networking, so its cruical for me to understand it once again.

So what is subnetting? Subnetting is the process in which you divide a large network into smaller managable parts that are referred to as subnets. We do this because it helps us organise a large enterprise, for an example, into departments such as I.T, Sales, HR, and etc. But this also has other benefits, such as increaseing security by isolating device groups, and improving the overall network performace by reducing the network broadcasting traffic.

IPv4 is used for subnetting. IPv4 can be split into 4 equal 8 bits:
```
   192   .    168   .     1    .     1
[8 Bits]   [8 Bits]   [8 Bits]   [8 Bits]
```
So subnets is what helps to define which part of the IP is the network and parts is for the hosts:
```
IP Address:     192.168.1.1
Subnet Mask:    255.255.255.0
```
Which converted into binary is:
```
IP:       11000000.10101000.00000001.00000001
Subnet:   11111111.11111111.11111111.00000000
```
> The reason why we convert the IPs into binary is because it enables us ot clearly resolve between the network and hosts portions of the address using the subnet mask, which is in binary. This conversion allows percies bitwise operations, such as AND operations, to calcuate network addresses, determine valid hosts ranges, and create or split subents accuractly. Since computers interpret and preocess data in binary, we have to convert the IPs into binary to ensure an accurate and efficient network calculations and configs.

So, the first 24 bits (counting all of the 1s in the Subnet `11111111.11111111.11111111`) are the network parts, and the remaining 8 Bits (the 8 0s at the end of the subnet `00000000`) are for the number of hosts. So there is 256 total addresses:
- 2^8 = 256
> NOTE: You must minus 256 by 2 because 1 is for network address `192.168.1.0` and the other is for the broadcast `192.168.1.255`. Leaving you with only 254 avaliable addresses.

Here are a few more examples:
| CIDR Notation | Default Netmask   | Subnet Binary                             |
|---------------|-------------------|-------------------------------------------|
| /8            | 255.0.0.0         | 11111111.00000000.00000000.00000000       |
| /16           | 255.255.0.0       | 11111111.11111111.00000000.00000000       |
| /24           | 255.255.255.0     | 11111111.11111111.11111111.00000000       |

So the smaller the CIDR Notation (might do a file on it), the more number of hosts avaliable.
- /8 = `11111111.00000000.00000000.00000000` (24 zeros)
- 2^24 = 16,777,216
- 16,777,216 - 2 = 16,777,214 avalaible hosts

The most important part of subnetting, in my opinion, is just understandoing how it works. The calcualation part can easily be done by using website for subnet calcualtions. 

 Keep in mind, this is not restricted to only 8 bits exact, its can be from 1 to 32 bits:
| Slash | Netmask           | 1st Octet | 2nd Octet | 3rd Octet | 4th Octet |
|--------|--------------------|------------|------------|------------|------------|
| /1     | 128.0.0.0          | 10000000   | 00000000   | 00000000   | 00000000   |
| /12    | 255.240.0.0        | 11111111   | 11110000   | 00000000   | 00000000   |
| /15    | 255.254.0.0        | 11111111   | 11111110   | 00000000   | 00000000   |
| /29    | 255.255.255.248    | 11111111   | 11111111   | 11111111   | 11111000   |

Now we can speak about the IP address classes. IP classes are 3 classes that split the IP address range into groups:
| Class | IP Range                    |
|-------|-----------------------------|
| A     | 1.0.0.0 to 127.0.0.0        |
| B     | 128.0.0.0 to 191.255.0.0    |
| C     | 192.0.0.0 to 223.255.255.0  |


### References:
- https://www.cbtnuggets.com/blog/technology/networking/networking-basics-what-is-ipv4-subnetting
- https://www.cloudflare.com/learning/network-layer/what-is-a-subnet/
- https://subnetipv4.com
- https://www.connecteddots.online/resources/blog/subnet-masks-table
