---

layout: post   
title: Saltstack net-api Runner/Local模块调用分析   
category: articles  
tags: [saltstack, api, runner, local]  
author: JackyWu  
comments: true  

---



背景:

该分析代码基于salt版本2015.5, 以下"/salt"为代码根目录.

源码路径在

{% highlight python linenos %}

    `https://github.com/saltstack/salt.git`中`/salt/netapi/rest_tornado` 

{% endhighlight %}

## Runner模块调用

runner模块之前的调用流程可以参考 [这里](/articles/salt-net-api源码分析/)

runner模块的调用接口是"/run", 匹配到saltnado.RunSaltAPIHandler类处理.

{% highlight python linenos %}

    /salt/salt/netapi/rest_tornado/saltnado.py

    RunSaltAPIHandler
        post()
    -> 
    SaltAPIHandler
        disbatch()
            ...
            chunk_ret = yield getattr(self, '_disbatch_{0}'.format(low['client']))(low)
            ret.append(chunk_ret)
            ...
    -> 以调用runner模块为例
    _disbatch_runner() , 这是yield这行代码获取到的函数名.
 
{% endhighlight %}

{% highlight python linenos %}

    /salt/salt/netapi/rest_tornado/saltnado.py
    
    @tornado.gen.coroutine
    def _disbatch_runner(self, chunk):
        '''
        Disbatch runner client commands
        '''
        f_call = {'args': [chunk['fun'], chunk]}
        pub_data = self.saltclients['runner'](chunk['fun'], chunk)
        tag = pub_data['tag'] + '/ret'
        try:
            event = yield self.application.event_listener.get_event(self, tag=tag)
            ...
        except TimeoutException:
            ...

{% endhighlight %}

在`_disbatch_runner`里调用了`self.saltclients['runner'](chunk['fun'], chunk)`, `self.saltclients['runner']`是什么可以在`class SaltClientsMixIn(object)`里找到,

{% highlight python linenos %}

    /salt/salt/netapi/rest_tornado/saltnado.py
    
    SaltClientsMixIn.__saltclients = {
        'local': local_client.run_job,
        # not the actual client we'll use.. but its what we'll use to get args
        'local_batch': local_client.cmd_batch,
        'local_async': local_client.run_job,
        'runner': salt.runner.RunnerClient(opts=self.application.opts).async,
        'runner_async': None,  # empty, since we use the same client as `runner`
        }
        
{% endhighlight %}

所以看`RunnerClient`的`async`方法.

{% highlight python linenos %}

    /salt/salt/client/mixins.py
    
    def async(self, fun, low, user='UNKNOWN'):
        '''
        Execute the function in a multiprocess and return the event tag to use
        to watch for the return
        '''
        async_pub = self._gen_async_pub()

        proc = multiprocessing.Process(
                target=self._proc_function,
                args=(fun, low, user, async_pub['tag'], async_pub['jid']))
        proc.start()
        proc.join()  # MUST join, otherwise we leave zombies all over
        return async_pub

{% endhighlight %}

调用了`self._proc_function`创建了一个进程去执行 `fun` , 然后将tag返回, 这个tag用来获取命令执行结果`event = yield self.application.event_listener.get_event(self, tag=tag)`.

真正执行fun函数的地方在

{% highlight python linenos %}

    /salt/salt/client/mixins.py
    
    class AsyncClientMixin(object):
        def _proc_function(self, fun, low, user, tag, jid, daemonize=True):
            ...
            return self.low(fun, low)
            ...
            
{% endhighlight %}

最底层的`self.low`方法调用.            

{% highlight python linenos %}

    /salt/salt/client/mixins.py

    def low(self, fun, low):
        ...
        data['return'] = self.functions[fun](*args, **kwargs)
        ...

{% endhighlight %}

小结

1. 通过上面的代码分析来看, 从net-api里的tornado到最终通过low()方法执行结果, 都是通过函数直接调用完成的, 没有通过rpc或者进程间通信. 所以只要你是想通过net-api执行runner模块,  net-api和saltmaster必须部署在同一台机器上.
1. 如果发现salt-api进程特别多, 那说明是`_proc_function`调用者特别多, 而该进程的执行时间又比较长, 所以这种情况下我们需要分析具体是调用了什么runner模块, 在这块进行优化.
1. 如果salt-api需要水平扩展, 则需要net-api + saltmaster一块扩展.
    

## 参考

- [salt net-api源代码](https://github.com/saltstack/salt.git)
- [PYTHON CLIENT API](https://docs.saltstack.com/en/latest/ref/clients/index.html#python-api)