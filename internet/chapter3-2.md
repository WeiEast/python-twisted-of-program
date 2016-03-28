###defer


#####1.succeed(result)
##### 这个函数非常有用，它返回一个Deferred对象，后面呢可以继续接回调函数，而且这个对象已经被callback过了。比如
   ```
   d=defer.succeed(0)
   d.addCallback(lambda _ : func())
   ```
#####因为d已经被执行过了，所以直接就可以进行下面的回调函数。

#####2.fail(result)
#####同理，这个是用来处理错误的errback的。

#####3.execute(callable, *args, **kw)
#####这个函数呢，通过callable这个可执行对象，来创建Deferred对象。

#####4.maybeDeferred(f, *args, **kw)
#####这个函数就是，当你不知道这个f是同步函数，还是异步函数的时候使用，统一返回Deferred对象。

#####5.inlineCallbacks(f)
#####这个呢，是一个装饰器，它的出现极大的简化了异步书写的流程，不必在用回调函数的形式来写异步代码。通过用python的yield来实现异步执行。
```
@defer.inlineCallbacks
def hello():
  r - yield async()＃这是一个异步回调函数
  defer.returnValue(r)
```
#####因为在函数内出现了yield就不能出现return，因此使用defer.returnValue来返回。这样就可以用同步的形式来书写异步代码。