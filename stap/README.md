

# README

Analysis and diagnoistcs tools for linux system based on [SystemTap](https://sourceware.org/systemtap/).


# Probes

[systemtap tabsets](https://sourceware.org/systemtap/tapsets/)

## Network Probes

syscall probe(s)
```
syscall.connect
```


socket probe(s):
```
socket.send
socket.receive
socket.sendmsg
socket.recvmsg
socket.aio_write
socket.aio_read
socket.write_iter
socket.read_iter
socket.writev
socket.readv
socket.create
socket.close
```



netdev probe(s):
```
netdev.open — Called when the device is opened
netdev.close — Called when the device is closed
netdev.register
netdev.unregister
netdev.rx  — Called when the device is going to receive a packet
netdev.receive — Data received from network device
netdev.transmit
netdev.hard_transmit
netdev.get_stats - Called when someone asks the device statistics
netdev.change_mtu
netdev.change_mac
netdev.change_rx_flag
netdev.set_promiscuity
netdev.ioctl
```


netfilter probe(s)
```
netfilter.ip.pre_routing
netfilter.ipv4.pre_routing
netfilter.ipv6.pre_routing
netfilter.ip.local_in
netfilter.ipv4.local_in
netfilter.ipv6.local_in
netfilter.ip.forward
netfilter.ipv4.forward
netfilter.ipv6.forward
netfilter.ip.local_out
netfilter.ipv4.local_out
netfilter.ipv6.local_out
netfilter.ip.post_routing
netfilter.ipv4.post_routing
netfilter.ipv6.post_routing
netfilter.arp.in
netfilter.arp.out
netfilter.arp.forward
netfilter.bridge.pre_routing
netfilter.bridge.local_in
netfilter.bridge.forward
netfilter.bridge.local_out
netfilter.bridge.post_routing
```


tcp probe(s)
```
tcp.sendmsg
tcp.recvmsg
tcp.disconnect
tcp.setsockopt
tcp.ipv4.setsockopt
tcp.ipv6.setsockopt
tcp.receive
tcp.ipv4.receive
tcp.ipv6.receive
```



udp probe(s)
```
udp.sendmsg
udp.recvmsg
udp.disconnect
```



ipmib probe(s)
```
ipmib.InReceives
ipmib.InUnknownProtos
ipmib.ForwDatagrams
ipmib.OutRequests
ipmib.ReasmTimeout
ipmib.ReasmReqds
```


some helper functions
```
function::format_ipaddr — Returns a string representation for an IP address
function::htonl — Convert 32-bit long from host to network order
function::htonll — Convert 64-bit long long from host to network order
function::htons — Convert 16-bit short from host to network order
function::ip_ntop — Returns a string representation for an IPv4 address
function::ntohl — Convert 32-bit long from network to host order
function::ntohll — Convert 64-bit long long from network to host order
function::ntohs — Convert 16-bit short from network to host order
```




# Kernel functions


## Network

```
probe kernel.function("*@net/socket.c").call
probe kernel.function("*@net/socket.c").return


probe kernel.function("sk_stream_wait_memory")
probe kernel.function("sk_stream_wait_memory").return
probe kernel.function("vfs_unlink").return
probe kernel.trace("kfree_skb")


probe kernel.{function("tcp_accept"),function("inet_csk_accept")}.return?
probe kernel.function("tcp_init_cwnd")
probe kernel.{function("tcp_rcv_established")
probe kernel.function("tcp_retransmit_skb")
probe kernel.function("tcp_set_state")
probe kernel.function("tcp_transmit_skb")


probe kernel.trace("net_dev_queue")
probe kernel.trace("net_dev_start_xmit")

```


# Scripts

[network questions](Network/questions)

[GO BACK](#README)


## Network Scripts

[oneliners scripts section1](Network/oneliners/oneliners-1-scripts) - scripts to list matching probes and local variables
<br/>
[oneliners scripts section1 output](Network/oneliners/oneliners-1-output.txt) - output to list matching probes and local variables

[oneliners scripts section2](Network/oneliners/oneliners-2-scripts) - scripts to show stacks of function
<br/>
[oneliners scripts section2 output](Network/oneliners/oneliners-2-output.txt) - output to show stacks of function

[oneliners scripts section3](Network/oneliners/oneliners-3-scripts) - scripts to trace
<br/>
[oneliners scripts section3 output](Network/oneliners/oneliners-3-output.txt) - output to trace   



[netdev](Network/netdev.stp) - Trace transmit/receive activity on network devices

[soconnect](Network/soconnect.stp)  - Trace the connect() socket call and latency

[tcp-accept-queue](Network/tcp-accept-queue.stp) - Tracing SYN && ACK backlog queue overflows on the listening port
<br/>
[tcp-retransmit-packet](Network/tcp-retransmit-packet.stp) - Tracing the tcp retransmission packet




