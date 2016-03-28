###protocol

#####1.ServerFactory
它是Factory的子类，通常我们都使用它。这里主要就是用来处理protocol的

######1.doStart 确保startFactory被调用
######2.doStop  确保stopFactory被调用
######3.startFactory 在监听端口前被调用，并且只会被调用一次
######4.stopFactory  在停止监听端口前被调用，且只被调用一次
######5.buldProtocol  创建一个protocol实例。


一般呢我们在startFactory里做一些服务器启动前做的准备，比如数据加载等。
在stopFactory里做一些为服务器关闭做的准备工作。


#####2.ClientCreator
client的连接, 三个方法分别连接不同的类型。
connectTCP，connectUnix，connectSSL。不需要factory。

#####3.ReconnectingClientFactory
看名字也知道，这是用来做重连接的。基本上和普通的factory是一样的，只不过加了重连接。


#####4.Protocol

这个是非常重要的一个类。我们一般使用他来处理数据, 连接等。

######1.ConnectionMade(): 建立连接，每当有一个client连接服务器，都会经过这个函数。可以
在这里做一些连接的管理，统计等。
######2.dataReceived(data):接受数据, 在这里来处理接受到的data。
######3.connectionLost()：当连接挂断，断线的时候，这个函数会被调用。可以在这里做一些
离线的操作，已经连接的管理。