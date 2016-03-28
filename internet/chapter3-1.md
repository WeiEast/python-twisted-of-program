###abstract

#####1.Class FileDescriptor
这是一个可以被select()用来操作的fd。

#####2.Function	isIPAddress	用来判断给出的字符串是否是ipv4的地址

#####3.Function	isIPv6Address	用来判断给出的字符串是否是ipv6的地址

这个库相对简单，用的时候也相对不太多，主要就是创建一个可以被select()的fd，已经判断ip地址的有效性。

eg: isIPAddress("192.168.1.111"), 参数是一个string.
