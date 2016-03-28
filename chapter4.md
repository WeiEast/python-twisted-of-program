####enterprise

#####adbapi

这里主要包含这样三个class, Connection(连接)，Transaction(事务)， ConnectionPool(连接池).

####1.Connection

里面主要包含三个函数,close，rollback，reconnect。
close用于关闭当前连接。
rollback用于回滚。
reconnect用于重连。

三个函数都没有参数，可以直接调用。