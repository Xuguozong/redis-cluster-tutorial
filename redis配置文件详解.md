## redis.conf 配置文件详解

    # 引入其它配置文件
    include /path/to/local.conf
    
    # 指定接受来自哪些ip的请求
    bind 0.0.0.0
    
    # 端口
    port 6379
    
    # 保护模式
    protected-mode yes
    
    # tcp-backlog 缺点TCP连接中已完成队列(3次握手)的长度，默认511,必须不大于/proc/sys/net/core/somaxconn值(128)
    # 修改此值：在/etc/sysctl.conf中添加 net.core.somaxconn=2048(高并发时),然后执行sysctl -p
    tcp-backlog 511
    
    # unixsock file路径和权限
    unixsocket /tmp/redis.sock
    unixsocketperm 700
    
    # 在客户端空闲N秒后关闭连接，0表示不关闭
    timeout 0
    
    # 单位是秒
    tcp-keepalive 300
    
    # 是否以守护进程运行
    daemonize no
    
    # 
    supervised no 
    
    # 以后台方式启动redis，需指定pid文件
    pidfile /var/run/redis_6379.pid
    
    # 日志级别 notice | debug | verbose | warning
    loglevel notice
    
    # 日志文件 | 以下情况为输出到标准输出
    logfile ""
    
    # 是否开启系统日志
    syslog-enabled no
    
    # 系统日志标识符
    syslog-ident redis
    
    # 日志来源、设备
    syslog-facility local0
    
    # 数据库数量，默认数据库是0，可用select选择一个
    database 16
    
    ##### 快照配置 #####
    
    # save [seconds] [changes]
    # 多少秒后至少有多少次key值改变就持久化数据
    save 900 1
    save 300 10
    save 60 10000
    
    # 持久化出错后是否依然持久化
    stop-writes-on-bgsave-error yes
    
    # 是否压缩rdb文件
    rdbcompression yes
    
    # 是否校验rbd文件(持久化时有10%性能损耗)
    rdbchecksum yes
    
    # 
    dbfilename dump.rdb
    
    # dir数据目录，rdb和aof都会在这个目录下
    dir ./
    
    ##### 主从复制配置 #####
    
    # slaveof [masterip] [masterport] 主机端口
    slaveof ip port
    
    # 主机密码
    masterauth ****
    
    # 当从节点失去连接或复制正在进行，从节点的2中运行方式
    # yes,继续响应客户端请求
    # no,除去info和slaveof命令其它请求都会返回错误
    slave-server-stale-data yes
    
    # 从服务器是否只读
    slave-read-only yes
    
