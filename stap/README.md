

# NAME

Analysis and diagnoistcs tools for linux system based on SystemTap.


# Probes


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
netdev.receive
netdev.transmit
netdev.change_mtu
netdev.open
netdev.close
netdev.hard_transmit
netdev.rx
netdev.change_rx_flag
netdev.set_promiscuity
netdev.ioctl
netdev.register
netdev.unregister
netdev.get_stats
netdev.change_mac
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



