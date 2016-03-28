# What is the twisted?


twisted是一个用python语言写的事件驱动的网络框架，他支持很多种协议，包括UDP,TCP,TLS和其他应用层协议，比如HTTP，SMTP，NNTM，IRC，XMPP/Jabber。 非常好的一点是twisted实现和很多应用层的协议，开发人员可以直接只用这些协议的实现。其实要修改Twisted的SSH服务器端实现非常简单。很多时候，开发人员只需要实现protocol类.