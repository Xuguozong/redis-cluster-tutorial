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
    
    ######################################## 快照配置 ############################
    
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
    
    ####################################### 主从复制配置 ################################
    
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
    
    # 是否使用socket方式复制数据
    # disk方式：多个slave共享rdb文件
    # socket方式：用socket顺序复制(适用磁盘慢，网络快)
    repl-diskless-sync no
    
    # socket复制延时时间
    repl-diskless-sync-delay 5
    
    # slave向master发起ping请求的时间间隔
    repl-ping-slave-period 10
    
    # 复制连接超时时间，要比上值大
    repl-timeout 60
    
    # 是否禁止复制tcp连接的tcp nodelay参数
    repl-disable-tcp-nodelay no
    
    # 复制缓冲区大小
    repl-backlog-size 1mb
    
    # master不再联系slave时释放backlog(内存)
    repl-backlog-ttl 3600
    
    # slave优先级
    slave-priority 100
    
    # 当健康的slave少于N，master就禁止写入
    min-slave-to-write 3
    
    # 延迟小于此的slave被认为是健康的
    min-slave-max-lag 10
    
    ##### 安全 #####
    requirepass [your pwd]
    
    ########################################## 客户端配置 ###########################
    
    # 能连上redis的最大数
    maxclients 10000
    
    # 最大内存容量
    maxmemory [nytes]
    
    # 内存达到上限的处理策略
    # volatile-lru:lru算法移除过期的key
    # volatile-random：随机移除过期的key
    # volatile-ttl：根据最近过期时间来删除
    # allkeys-lru：lru算法移除所有key
    # allkeys-random:随机移除任何key
    # noeviction:不移除key，只返回一个写错误
    maxmemory noeviction
    
    ######################################### 持久化配置 #######################
    
    # 是否启用aof(Append Only File)模式
    appendonly yes
    
    # aof文件名称
    appendfilename "appendonly.aof"
    
    # aof持久化策略
    # no
    # always
    # everysec
    appendfsync everysec
    
    # 
    no-appendfsync-on-rewrite no
    
    # 当前aof大小超过之前重写的aof大小的百分值多少在进行重写
    auto-aof-rewrite-percentage 100
    # 允许重写的最小aof大小
    auto-aof-rewrite-min-size 64mb
    
    # redis启动时是否加载截断的aof文件
    aof-load-truncated yes
    
    ########################################## 集群设置 #############################3
    
    # 是否开启集群
    cluster-enabled yes
    
    # 集群配置文件，无需自己编辑
    cluster-config-file nodes.conf
    
    # 节点间连接的超时时间
    cluster-node-timeout 15000
    
    # 用来判断slave是否有master断开连接过长，导致slave数据陈旧在故障转移的时候不能用
    # 失效校验次数
    cluster-slave-validity-factor 1
    
    # 集群是否要求全slots覆盖
    cluster-require-full-coverage no
    
    # 主节点需要的最小从节点数
    cluster-migration-barrier 1
    
    ############################################ 慢日志 #################################
    
    # 慢查询时间
    slowlog-log-slower-than 10000
    
    # 慢查询日志长度
    slowlog-max-len 128
    
    # 延迟监控（0表示关闭）
    latency-monitor-threshold 0
