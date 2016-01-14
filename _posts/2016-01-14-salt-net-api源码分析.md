---

layout: post   
title: Saltstack net-api 源码分析   
category: articles  
tags: [saltstack, api]  
author: JackyWu  
comments: true  

---

# 背景

该分析代码基于salt版本2015.5, 以下"/salt"为代码根目录.

源码路径在

    `https://github.com/saltstack/salt.git`中`/salt/netapi/rest_tornado`

# 启动脚本

启动命令

    `/salt/pkg/rpm/salt-api`  or  `/etc/init.d/salt-api`
    `daemon --pidfile=/var/run/salt-api.pid --check salt-api /usr/bin/salt-api -d`

其他启动参数

    # salt-api --help

# 代码入口

入口代码为

    /salt/scripts/salt-api (/usr/bin/salt-api)
    ->
    /salt/salt/scripts.py
    -> 
    /salt/salt/cli/api.py
        SaltAPI.setup_config() 寻找/etc/salt/master文件进行配置设置
        ->
            /salt/salt/config.py
                api_config() -> client_config()
        ->
        SaltAPI.run():
            - parse_args()
            - /salt/salt/utils/parsers.py LogLevelMixIn.setup_logfile_logger()
            ->
            /salt/salt/client/netapi.py  NetapiClient
                self.process_manager = ProcessManager()
                self.netapi -> /salt/salt/loader.py LazyLoader : load rest_tornado模块
                self.process_manager.run()
进入tornado

    /salt/salt/netapi/rest_tornado/__init__.py
        start()
            ```
           paths = [
            (r"/", saltnado.SaltAPIHandler),
            (r"/login", saltnado.SaltAuthHandler),
            (r"/minions/(.*)", saltnado.MinionSaltAPIHandler),
            (r"/minions", saltnado.MinionSaltAPIHandler),
            (r"/jobs/(.*)", saltnado.JobsSaltAPIHandler),
            (r"/jobs", saltnado.JobsSaltAPIHandler),
            (r"/run", saltnado.RunSaltAPIHandler),
            (r"/events", saltnado.EventsSaltAPIHandler),
            (r"/hook(/.*)?", saltnado.WebhookSaltAPIHandler),
            ] 
            ```

以"/run"接口为例, 调用saltnado.RunSaltAPIHandler类

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
    _disbatch_runner() 给SaltMaster发命令, 执行, 返回结果.


# 参考资料

- [salt net-api源代码](https://github.com/saltstack/salt.git)
