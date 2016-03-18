###reactor
#####reactor是twisted的event循环，也是整个app的驱动。reactor提供许多在线程，网络，事件等api。

1.run
  reactor.run()，启动reactor事件循环
  
2.stop
  对应的,停止事件循环
  
3.running
  判断当前reactor是否正在运行，如果是则返回True，否则为False
  
4.addSystemEventTrigger（phase, eventType, callable, *args, **kw）

  当system事件发生的时候，执行添加的function。系统事件，比如start,stop等。通常呢，我们用做在服务器关闭的时候，
  添加一些函数，用来处理数据入库等操作，保证服务器关闭的时候，内存数据不会丢失。
  
  phase就是执行func的时机，有"before", "after", "during"三种。很好理解，当系统事件发生的时候，在之前，之后还是
  进行时去执行func。
  eventType就是对于这个事件的描述，比如"shutdown"，服务器关闭。"startup"， 服务器开启。注意，这里是string
  callable就是要执行的函数，后面就是他的参数
  
  eg:
      reactor.addSystemEventTrigger("before", "shutdown", helloworld)#这就是在服务器关闭之前去执行helloworld函数。
 
5.removeSystemEventTrigger
6.callWhenRunning