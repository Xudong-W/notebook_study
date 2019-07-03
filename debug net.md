1 查看MTU
	在本机打开dos窗口，执行：ping -f -l 1472 192.168.0.1
	其中192.168.0.1是网关IP地址，1472是数据包的长度。请注意，上面的参数是“-l”（小写的L），而不是“-1”。
	如果能ping通，表示数据包不需要拆包，可以通过网关发送出去。
	如果出现：Packet needs to be fragmented but DF set.表示数据包需要拆开来发送。此时，减少数据包长度，再执行上面的ping命令。从1400到1472之间多试几次，就能找到合适的数据包长度了。把数据包长度加上数据包头28字节，就得到MTU的值。

2 netstat(unix高级网络编程)

3 ps （unix高级网络编程）

4 nslookup  (name server lookup) 域名解析  查找对应域名的IP地址，或ping 域名

5 traceroute