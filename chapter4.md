####enterprise

#####adbapi

这里主要包含这样三个class, Connection(连接)，Transaction(事务)， ConnectionPool(连接池).

####1.Connection

里面主要包含三个函数,close，rollback，reconnect。
close用于关闭当前连接。
rollback用于回滚。
reconnect用于重连。

三个函数都没有参数，可以直接调用。

####2.Transaction
也有三个函数，close, reopen, reconnect.即关闭，重打开，重新连接



####3.ConnectionPool
这个是最常用的，包含以下几个函数。
start， 开启当前连接池
runWithConnection(func, *args, **kw)使用当前的连接执行一个函数,并且返回result
runInteraction(interaction, *args, **kw)与数据库交互，interaction是一个事务对象
runQuery
runOperation
close
finalClose
connect	
disconnect