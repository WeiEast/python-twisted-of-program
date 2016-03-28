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
runQuery(*args, **kw)执行sql语句，并返回result
runOperation(*args, **lw) 执行sql语句，并返回None
close, 关闭当前连接池
finalClose。 应该被服务器关闭的触发器调用
connect	返回的是数据库连接对象。
disconnect(conn) 关闭连接池中的某个连接

我是例子：
```
class ReconnectingConnectionPool(adbapi.ConnectionPool):
    def _runInteraction(self, interaction, *args, **kw):
        conn = self.connectionFactory(self)
        trans = self.transactionFactory(self, conn)

        try:
            result = interaction(trans, *args, **kw)
            trans.close()
            conn.commit()
            return result
        except MySQLdb.OperationalError, e:
            if e[0] in (2006, 2013):
                log.info("RCP: got error %s, retrying operation" %(e))
                conn = self.connections.get(self.threadID())
                self.disconnect(conn)
                return self._runInteraction(interaction, *args, **kw)
            else:
                #traceback.print_exc()
                excType, excValue, excTraceback = sys.exc_info()
                try:
                    conn.rollback()
                except Exception, e:
                    log.exception("Roll failed.")

                raise excType, excValue, excTraceback
        except:
            #traceback.print_exc()
            excType, excValue, excTraceback = sys.exc_info()
            raise excType, excValue, excTraceback```

这个类返回的是连接池对象，实例化以后，就可以直接使用这个对象
比如
dbpool = ReconnectingConnectionPool('MySQLdb', **config)
dbpool.runQuery(sql)
可以自己封装一个class, 用来包装一些常用的db操作