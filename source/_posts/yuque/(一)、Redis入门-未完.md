
---

title: (一)、Redis入门-未完

date: 2019-05-25 16:41:00 +0800

tags: [Redis,Nosql]

categories: Redis

---


Redis 是一个高性能的key-value数据库, 支持主从同步, 完全实现了发布/订阅机制, 因此可以用于聊天室等场景. 主要表现于多个浏览器之间的信息同步和实时更新.
> <br />和Memcached类似，它支持存储的value类型相对更多，包括 `string(字符串)` 、 `list(链表)` 、 `set(集合)` 、 `zset(sorted set –有序集合)` 和 `hash（哈希类型）` 。这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。数据可以从master向任意数量的slave上同步，slave可以是关联其他slave的master。这使得Redis可执行单层树复制。存盘可以有意无意的对数据进行写操作。由于完全实现了发布/订阅机制，使得slave在任何地方同步树时，可订阅一个频道并接收master完整的消息发布记录。同步对读取操作的可扩展性和数据冗余很有帮助.

<a name="gZXnH"></a>
# 特点、优势

- k、v键值存储以及数据结构存储（如列表、字典）
- 所有数据(包括数据的存储)操作均在内存中完成
- 单线程服务(这意味着会有较多的阻塞情况)，采用epoll模型进行请求响应，对比nginx
- 支持主从复制模式，更提供高可用主从复制模式（哨兵）
- 去中心化分布式集群
- 丰富的编程接口支持，如Python、Golang、Java、php、Ruby、Lua、Node.js 
- 功能丰富，除了支持多种数据结构之外，还支持事务、发布/订阅、消息队列等功能
- 支持数据持久化(AOF、RDB)
<a name="blogTitle4"></a>
### 对比memcache

- memcache是一个分布式的内存对象缓存系统，并不提供持久存储功能，而redis拥有持久化功能
- memcache数据存储基于LRU(简单说：最近、最少使用key会被剔除)，而redis则可以永久保存(服务一直运行情况下)
- memcache是多线程的（这是memcache优势之一），也就意味着阻塞情况少，而redis是单线程的，阻塞情况相对较多
- 两者性能上相差不大
- memcache只支持简单的k、v数据存储，而redis支持多种数据格式存储。
- memcache是多线程、非阻塞IO复用网络模型，而redis是单线程IO复用模型
<a name="R2QxJ"></a>
# 安装
<a name="bcrEp"></a>
## linux下安装

```basic
yum install gcc -y  # 安装C依赖
wget http://download.redis.io/redis-stable.tar.gz  # 下载稳定版本
tar zxvf redis-stable.tar.gz  # 解压
cd redis-stable
make PREFIX=/opt/app/redis install   # 指定目录编译，也可以不用指定
make install
mkdir /etc/redis   # 建立配置目录
cp redis.conf /etc/redis/6379.conf # 拷贝配置文件 （from to）
cp utils/redis_init_script /etc/init.d/redis  # 拷贝init启动脚本针对6.X系统
chmod a+x  /etc/init.d/redis  # 添加执行权限
vi /etc/redis/6379.conf # 修改配置文件： 
bind 0.0.0.0      # 监听地址
maxmemory 4294967296   # 限制最大内存（4G）：
daemonize yes   # 后台运行

####启动与停止
/etc/init.d/redis start
/etc/init.d/redis stop
```
查看是否安装成功

```basic
#执行客户端工具
redis-cli 
#输入命令info
127.0.0.1:6379> info
# Server
redis_version:4.0.10
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:cf83e9c690dbed33
redis_mode:standalone
os:Linux 2.6.32-642.el6.x86_64 x86_64
arch_bits:64
multiplexing_api:epoll
```

<a name="O5Hdg"></a>
## windows下安装
Redis官方下载的redis是不支持windows版本的。微软公司也开发了自己的redis，但是官方Redis对微软公司开发的redis不提供技术服务。微软的redis只能供练习使用。
<a name="JhIMz"></a>
## 二进制文件说明
redis安装完成后会有以下可执行文件（window下是exe文件）生成，下面是各个文件的作用。

```basic
redis-server　　　　   #Redis服务器和Sentinel服务器，启动时候可使用--sentinel指定为哨兵
redis-cli　　　　　    #Redis命令行客户端 
redis-benchmark　     #Redis性能测试工具 
redis-check-aof      #AOF文件修复工具 
redis-check-dump     #RDB文件检测工具 
redis-sentinel       #Sentinel服务器,4.0版本已经做了软链接到redis-server
```

<a name="1hWZE"></a>
# 启动
<a name="ubG81"></a>
## linux下

```powershell
语法: ./redis-server  redis.conf
```
<a name="HjJgE"></a>
## windows下

```powershell
服务器启动；
    语法: ./redis-server  redis.conf
客户端启动；
   ./redis-cli [-h 主机地址] [-p 端口号]  默认端口:6379
```

<a name="5wrcW"></a>
# 配置详解
redis所有的配置参数都可以通过客户端通过“CONFIG GET 参数名” 获取，参数名支持通配符，如*代表所有。所得结果并按照顺序分组，第一个返回结果是参数名，第二个结果是参数对应的值。

```basic
127.0.0.1:6379> config get *
1) "dbfilename"     # 参数名
2) "dump.rdb"       # dbfilename的值为dump.rdb
  3) "requirepass"
  4) ""
  5) "masterauth"
  6) ""
  7) "unixsocket"
  8) ""
  9) "logfile"
 10) ""
```
除了查看配置还可以使用CONFIG SET修改配置，写入配置文件使用CONFIG REWRITE,使用时是需要注意某些关于服务配置参数慎重修改，如bind

```basic
127.0.0.1:6379> config set dbfilename back.rdb
OK
127.0.0.1:6379> config rewrite
OK
127.0.0.1:6379> config get dbfilename
1) "dbfilename"
2) "back.rdb"
```
配置参数以及解释，需要注意的是，有些配置是4.0.10新增的，有些配置已经废除，如vm相关配置，和集群相关配置在集群篇章在进行补充。

```basic
logfile
#日志文件位置及文件名称

bind 0.0.0.0
#监听地址，可以有多个 如bind 0.0.0.0 127.0.0.1

daemonize yes
#yes启动守护进程运行，即后台运行，no表示不启用

pidfile /var/run/redis.pid 
# 当redis在后台运行的时候，Redis默认会把pid文件在在/var/run/redis.pid，也可以配置到其他地方。
# 当运行多个redis服务时，需要指定不同的pid文件和端口

port 6379
# 指定redis运行的端口，默认是6379

unixsocket 
#sock文件位置

unixsocketperm
#sock文件权限

timeout 0
# 设置客户端连接时的超时时间，单位为秒。当客户端在这段时间内没有发出任何指令，那么关闭该连接，
0是关闭此设置

loglevel debug
# 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose

logfile ""
# 日志文件配置,默认值为stdout，标准输出，若后台模式会输出到/dev/null

syslog-enabled
# 是否以syslog方式记录日志，yes开启no禁用，与该配置相关配置syslog-ident 和syslog-facility local0 
分别是指明syslog的ident和facility

databases 16
#配置可用的数据库个数，默认值为16，默认数据库为0，数据库范围在0-（database-1）之间

always-show-logo yes #4.0以后新增配置
#是否配置日志显示redis徽标，yes显示no不显示


################################ 快照相关配置 #################################

save 900 1
save 300 10
save 60 10000
#配置快照(rdb)促发规则，格式：save <seconds> <changes>
#save 900 1  900秒内至少有1个key被改变则做一次快照
#save 300 10  300秒内至少有10个key被改变则做一次快照
#save 60 10000  60秒内至少有10000个key被改变则做一次快照

dbfilename  dump.rdb
#rdb持久化存储数据库文件名，默认为dump.rdb

stop-write-on-bgsave-error yes 
#yes代表当使用bgsave命令持久化出错时候停止写RDB快照文件，no则代表继续写

rdbchecksum yes
#开启rdb文件校验

dir "/etc"
#数据文件存放目录，rdb快照文件和aof文件都会存放至该目录


################################# 复制相关配置参数 #################################

slaveof <masterip> <masterport>  
#设置该数据库为其他数据库的从数据库，设置当本机为slave服务时，设置master服务的IP地址及端口，
在Redis启动时，它会自动从master进行数据同步

masterauth <master-password>
#主从复制中，设置连接master服务器的密码（前提master启用了认证）

slave-serve-stale-data yes
# 当从库同主机失去连接或者复制正在进行，从机库有两种运行方式：
# 1) 如果slave-serve-stale-data设置为yes(默认设置)，从库会继续相应客户端的请求
# 2) 如果slave-serve-stale-data是指为no，除了INFO和SLAVOF命令之外的任何请求都会返回一个
错误"SYNC with master in progress"

repl-ping-slave-period 10
#从库会按照一个时间间隔向主库发送PING命令来判断主服务器是否在线，默认是10秒

repl-timeout 60
#设置主库批量数据传输时间或者ping回复时间间隔超时时间，默认值是60秒
# 一定要确保repl-timeout大于repl-ping-slave-period

repl-backlog-size 1mb
#设置复制积压大小,只有当至少有一个从库连入才会释放。

slave-priority 100
#当主库发生宕机时候，哨兵会选择优先级最高的一个称为主库，从库优先级配置默认100，数值越小优先级越高

min-slaves-to-write 3
min-slaves-max-lag 10
#设置某个时间段内，如果从库数量小于该某个值则不允许主机进行写操作，以上参数表示10秒内如果主库的从节点
小于3个，则主库不接受写请求，min-slaves-to-write 0代表关闭此功能。


################################## 安全相关配置 ###################################

requirepass
#客户端连接认证的密码，默认为空，即不需要密码，若配置则命令行使用AUTH进行认证。配置密码，即直接在
其后跟上要用的密码即可

maxclients 10000
# 设置同一时间最大客户端连接数，4.0默认10000，Redis可以同时打开的客户端连接数为Redis进程可以打开的
最大文件描述符数，
# 如果设置 maxclients 0，表示不作限制。
# 当客户端连接数到达限制时，Redis会关闭新的连接并向客户端返回max number of clients reached错误信息

maxmemory 4gb
#设置最大使用的内存大小

maxmemory-policy noeviction
#设置达到最大内存采取的策略：
# volatile-lru -> 利用LRU算法移除设置过过期时间的key (LRU:最近使用 Least Recently Used )
# allkeys-lru -> 利用LRU算法移除任何key
# volatile-random -> 移除设置过过期时间的随机key
# allkeys->random -> remove a random key, any key
# volatile-ttl -> 移除即将过期的key(minor TTL)
# 4.0默认noeviction代表不删除任何key，只在写操作时候返回错误。

maxmemory-samples 5
#LRU，LFU等算法样本设置，默认5个key


############################## AOF相关配置###############################

appendonly no
# 设置AOF持久化，yes开启，no禁用，开启后redis会把所接收到的每一次写操作请求都追加到appendonly.aof
文件中，当redis重新启动时，会从该文件恢复出之前的状态。
# 但是这样会造成appendonly.aof文件过大，所以redis还支持了BGREWRITEAOF指令，对appendonly.aof 
进行重写。

appendfilename "appendonly.aof"
#设置AOF文件名

appendfsync everysec
# AOF文件写策略，Redis支持三种同步AOF文件的策略:
# no: 不进行同步，交给操作系统去执行 ，速度较快
# always: always表示每次有写操作都调用fsync方法强制内核将该写操作写入到文件，速度会慢, 但是安全，
因为每次写操作都在AOF文件中.
# everysec: 表示对写操作进行累积，每秒同步一次，折中方案.
# 默认是"everysec"，按照速度和安全折中这是最好的。

no-appendfsync-on-rewrite no
# AOF策略设置为always或者everysec时，后台处理进程(后台保存或者AOF日志重写)会执行大量的I/O操作
# 在某些Linux配置中会阻止过长的fsync()请求。注意现在没有任何修复，即使fsync在另外一个线程进行处理，
为了减缓这个问题，可以设置下面这个参数no-appendfsync-on-rewrite

auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb
#当AOF文件增长到一定大小的时候Redis能够调用BGREWRITEAOF对日志文件进行重写，它是这样工作的：Redis
会记住上次进行些日志后文件的大小(如果从开机以来还没进行过重写，那日子大小在开机的时候确定)。
#基础大小会同现在的大小进行比较。如果现在的大小比基础大小大制定的百分比，重写功能将启动
# 同时需要指定一个最小大小用于AOF重写，这个用于阻止即使文件很小但是增长幅度很大也去重写AOF文件的情况
# 设置 percentage 为0就关闭这个特性
#auto-aof-rewrite-percentage 代表AOF文件每次重写文件大小（以百分数代表），100表示百分之百，即当
文件增加了1倍（100%），则开始重写AOF文件
#auto-aof-rewrite-min-size  设置最小重写文件大小，避免文件小而执行太多次的重写

aof-load-truncated yes
＃当redis突然运行崩溃时，会出现aof文件被截断的情况，Redis可以在发生这种情况时退出并加载错误，以下
选项控制此行为。
＃如果aof-load-truncated设置为yes，则加载截断的AOF文件，Redis服务器启动发出日志以通知用户该事件。
＃否则，如果该选项设置为no，则服务器将中止并显示错误并停止启动。当该选项设置为no时，用户需要在重启之前
使用“redis-check-aof”实用程序修复AOF文件再进行重启


################################## 慢查询配置 ###################################


slowlog-log-slower-than 10000
 #Redis Slow Log 记录超过特定执行时间的命令。执行时间不包括I/O计算比如连接客户端，返回结果等，
只是命令执行时间，可以通过两个参数设置slow log：一个是告诉Redis执行超过多少时间被记录的参数
slowlog-log-slower-than(微秒，因此1000000代表一分钟
#另一个是slow log 的长度。当一个新命令被记录的时候最早的命令将被从队列中移除
 
slowlog-max-len 128
#慢查询命令记录队列长度设置，该队列占用内存，可以使用SLOWLOG RESET清空队列



############################### 高级配置 ###############################

hash-max-zipmap-entries 512
hash-max-zipmap-value 64
# 当hash中包含超过指定元素个数并且最大的元素没有超过临界时，hash将以一种特殊的编码方式
（大大减少内存使用）来存储，这里可以设置这两个临界值
# Redis Hash对应Value内部实际就是一个HashMap，实际这里会有2种不同实现，
# 这个Hash的成员比较少时Redis为了节省内存会采用类似一维数组的方式来紧凑存储，而不会采用
真正的HashMap结构，对应的value redisObject的encoding为zipmap,当成员数量增大时会自动转成真正
的HashMap,此时encoding为ht。

list-max-ziplist-size -2
#Lists也以特殊方式编码，以节省大量空间。
＃可以指定每个内部列表节点允许的条目数
＃作为固定的最大大小或最大元素数。
＃对于固定的最大大小，使用-5到-1表示：
＃-5：最大大小：64 Kb < - 不建议用于正常工作负载
＃-4：最大尺寸：32 Kb < - 不推荐
＃-3：最大尺寸：16 Kb < - 可能不推荐
＃-2：最大尺寸：8 Kb < - 好
＃-1：最大尺寸：4 Kb < - 良好
＃正数意味着存储_exactly_元素数量
＃每个列表节点。
＃性能最高的选项通常为-2（8 Kb大小）或-1（4 Kb大小）

zset-max-ziplist-entries 128
zset-max-ziplist-value 64
# list数据类型多少节点以下会采用去指针的紧凑存储格式。
# list数据类型节点值大小小于多少字节会采用紧凑存储格式。

activerehashing yes
# Redis将在每100毫秒时使用1毫秒的CPU时间来对redis的hash表进行重新hash，可以降低内存的使用
# 当你的使用场景中，有非常严格的实时性需要，不能够接受Redis时不时的对请求有2毫秒的延迟的话，把
这项配置为no。
# 如果没有这么严格的实时性要求，可以设置为yes，以便能够尽可能快的释放内存

client-output-buffer-limit normal 0 0 0
client-output-buffer-limit slave 256mb 64mb 60
client-output-buffer-limit pubsub 32mb 8mb 60
#客户端输出缓冲区限制可用于强制断开客户端，由于某种原因，没有足够快地从服务器读取数据，常见的原因
是Pub / Sub客户端不能像很快的消费一条消息，可以为三种不同类型的客户端设置不同的限制：
#normal - >普通客户端，包括MONITOR客户端
#subve - >从服务器客户端
#pubsub - >客户端订阅了至少一个pubsub通道或模式
#设置方法：client-output-buffer-limit 软限制大小 硬限制大小 秒数
#当客户端达到硬限制大小则立即断开连接，当客户端达到软限制时候并且在设置的秒数缓冲大小任然超了，
  则在设置的秒数后断开连接
```

<a name="M2KUq"></a>
# 操作数据类型
redis的数据都是以key-value的形式存储的, 因此`get/set`操作是使用最常见的。
<a name="hgyxP"></a>
## 命令使用前言-redis帮助
通大多数据库一样，redis所有的命令提供了帮助，可以使用 help +命令名称 查看其使用方法，帮助信息中不仅有命令用法，还有命令始于版本信息，分组等。

为了友好的使用，redis还将所有命令都进行了分组,同时使用help+@+组名进行查看每个组中所有命令，以下是所有分组信息。

```basic
127.0.0.1:6379> help
redis-cli 3.2.100
To get help about Redis commands type:
      "help @<group>" to get a list of commands in <group>
      "help <command>" for help on <command>
      "help <tab>" to get a list of possible help topics
      "quit" to exit

To set redis-cli perferences:
      ":set hints" enable online hints
      ":set nohints" disable online hints
Set your preferences in ~/.redisclirc
127.0.0.1:6379> help get

  GET key
  summary: Get the value of a key
  since: 1.0.0
  group: string
```

上面以及介绍如何查看命令使用方法，所以在以下数据类型操作时候，只举例常用的命令，更多命令参考 <br />https://redis.io/commands<br />
<br />注意：redis在3.2版本新增geo数据类型。

```basic
generic       #一般命令组，对大多数类型适用
string        #字符串类型命令组，使用所有字符串类型
list          #列表类型命令组
set           #集合类型命令组
sorted_set    #有序集合命令组
hash          #hash操作命令组
pubsub        #发布命令组
transactions  #事务操作命令组
connection    #连接相关命令组
server        #服务器相关命令组
scripting     #lua 脚本命令组
hyperloglog   #hyperloglog类型命令组，redis在 2.8.9 版本添加了 HyperLogLog 结构
cluster       #集群相关命令组
geo           #经纬度相关命令组，适用于3.2.0以后的版本
```
示例：查看事务操作所有命令

```basic
127.0.0.1:6379> help @transactions

  DISCARD -
  summary: Discard all commands issued after MULTI
  since: 2.0.0

  EXEC -
  summary: Execute all commands issued after MULTI
  since: 1.2.0

  MULTI -
  summary: Mark the start of a transaction block
  since: 1.2.0

  UNWATCH -
  summary: Forget about all watched keys
  since: 2.2.0

  WATCH key [key ...]
  summary: Watch the given keys to determine execution of the MULTI/EXEC block
  since: 2.2.0
```
<a name="eftXG"></a>
## 与key有关的操作
命名规则：除了空格、换行不能键名，其他都能做键。

常用:

```basic
DEL key [key ...] # 删除某个key，支持多个key,删除成功返回个数
KEYS pattern  # 查看符合正则的所有key
EXISTS key [key ...] # 判断某个key是否存在，可支持多个，返回存在的个数
EXPIRE key seconds # 刷新某个key过期时间
ttl key # 检测key剩余的过期时间
select db_index # 选择数据库，在redis中最多有16个数据库，在配置文件redis.conf 搜索【database】查看。
  # 编号从0-15。默认当前数据库是0
move key db_index  # 移动key到某个数据库
rename key newkey # 给key重命名
type key # 返回键值对应的类型
randomkey # 从现有key中随机的返回一个
```
实例:

```basic
127.0.0.1:6379> keys * # 查看符合正则的所有key
age
sex
city
list1
hello
school
name
list2
127.0.0.1:6379> keys l*  # 查看符合正则的所有key
list1
list2
127.0.0.1:6379> del school age # 删除某个key，支持多个key
1
127.0.0.1:6379> keys *
sex
city
list1
hello
school
name
127.0.0.1:6379> exists school # 判断某个key是否存在，可支持多个，返回存在的个数
0
127.0.0.1:6379> exists school sex # 判断多个key是否存在，返回存在的个数
1
127.0.0.1:6379> type list1 # 查看类型，这个是list类型
list
127.0.0.1:6379> type sex # 查看类型，这个是string类型的
string
127.0.0.1:6379> randomkey  # 从现有key中随机的返回一个
list1 
127.0.0.1:6379> randomkey # 从现有key中随机的返回一个
list2
127.0.0.1:6379> rename list2 list3 # 给key改名
OK
127.0.0.1:6379> keys *
sex
city
list1
hello
list3
name
# 刷新key并检测过期时间
127.0.0.1:6379> expire list3 12
1
127.0.0.1:6379> ttl list3
2
127.0.0.1:6379> ttl list3
-2
127.0.0.1:6379> ttl list3
-2
# 移动key到某个数据库并查看
127.0.0.1:6379> keys *   # 当前数据库0 
sex
city
list1
hello
name
127.0.0.1:6379> move city 2 # 移动到数据库2
1
127.0.0.1:6379> select 2 # 选择数据库2 
OK
127.0.0.1:6379[2]> keys * # 查看数据库2的key
city
```

<a name="O3zdr"></a>
## 对string的操作

1. string可以保存任何数据，包括数字、图片、序列化的对象
1. redis中的整型也当作字符串处理

常用:

```basic
set key value [EX seconds] [PX milliseconds] [NX|XX]  # 设置key为指定的字符串值。
# 参数：
# EX seconds – 设置键key的过期时间，单位是秒
# PX milliseconds – 设置键key的过期时间，单位是毫秒
# NX – 只有键key不存在的时候才会设置key的值
# XX – 只有键key存在的时候才会设置key的值

append key value  # 如果 key 已经存在，并且值为字符串，那么这个命令会把 value 追加到原来值（value）的
结尾。 如果 key 不存在，那么它将首先创建一个空字符串的key，再执行追加操作，这种情况 APPEND 将类似
于 SET 操作。

get key #获取key值，不存在则返回nil

getrange key start end # 获取指定key值的索引开始位置和结束位置所对应的值，索引从0开始

getset key value  # 设置新的key值，并获取设置之前的值，如果key不存在则设置，并返回nil

mget key [key ...]   # 批量获取key的值

mset key value [key value ...] # 批量设置key的值

decr key #数字类型的key自减操作，key类型不是数字则报错

incr key  # 数字类型key 自加操作，与DECR相反

decrby key decrement  #数字类型key指定减少数值

incrby key increment   #数字类型key指定增加数值，与DECRBY相反

strlen key  # 获取key长度
```
实例:
```basic
127.0.0.1:6379> set hello world # 设置hello的值为world
OK
127.0.0.1:6379> get hello # 查看hello的值
world
127.0.0.1:6379> type hello # 值类型
string
127.0.0.1:6379> set age 10 EX 6  # 设置age为10，并在6秒后过期
OK
127.0.0.1:6379> ttl age
(integer) 2
127.0.0.1:6379> ttl age
(integer) -2
127.0.0.1:6379> ttl age
(integer) -2
127.0.0.1:6379> substr hello 1 2 # 截取值，小标从0开始，开始的下标，结束的下标
or
127.0.0.1:6379> append hello !!!  # 字符串追加
8
127.0.0.1:6379> get hello
world!!!
127.0.0.1:6379> getrange hello 1 3 # 获取指定key值的索引开始位置和结束位置所对应的值，索引从0开始
"orl"
# 设置新的key值，并获取设置之前的值，如果key不存在则设置，并返回nil
127.0.0.1:6379> get hello
"world!!!"
127.0.0.1:6379> getset hello 22 # 设置新值为22，并返回之前的值
"world!!!"
127.0.0.1:6379> get hello
"22"
# 批量获取
127.0.0.1:6379> mget school hello
1) (nil)
2) "22"
# 批量设置
127.0.0.1:6379> mset k1 v1 k2 v2
OK
127.0.0.1:6379> mget k1 k2
1) "v1"
2) "v2"

127.0.0.1:6379> set haha heiheihei # 新建key
OK
127.0.0.1:6379> set name tom # 新建key
OK
127.0.0.1:6379> del name # 删除键，可以一次删多个；删除成功返回个数
1
127.0.0.1:6379> keys *
hello
```
<a name="Y5yqc"></a>
## 对list的操作
redis中的list在底层实现上是链表. 因此, 无论list的空间复杂度是多少, 其时间复杂度是常数级别的. 即使用lpush在10个元素的list头部插入新元素, 和在上万个元素的lists头部插入新元素的速度相当. 但lists中的元素定位会比较慢.

列表中的元素索引从0开始，倒数的元素可以用“-”+倒数位置表示，如-2，代表倒数第二个元素，-1则代表最后一个元素。<br />
<br />Redis列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边。<br />一个列表最多可以包含 2 - 1 个元素 (4294967295, 每个列表超过40亿个元素)。<br />

> 常见操作有lpush, rpush, lrange等.
> 

```basic
127.0.0.1:6379> keys *
hello
127.0.0.1:6379> lpush list1 1  # 链表头部插入数据1
1
127.0.0.1:6379> lpush list1 2 # 链表头部插入数据2
2
127.0.0.1:6379> rpush list1 0 #  链表尾部插入数据
3
127.0.0.1:6379> llen list1 # 链表长度
3
127.0.0.1:6379> lrange list1 0 1 # 列出编号0~1的元素
2
1
127.0.0.1:6379> lrange list1 0 -1 # 列出编号0到倒数第一个元素
2
1
0
127.0.0.1:6379> keys *
hello
list1
127.0.0.1:6379> type list1
list
127.0.0.1:6379> lindex list1 0 # 根据索引从list中获取元素
2
127.0.0.1:6379> lindex list1 -1 # 根据索引从list中获取元素
0
127.0.0.1:6379> lset list1 0 -8 # 根据索引设置列表中元素的值,当list不存在时报错
OK
127.0.0.1:6379> lindex list1 0 # 根据索引获得值
-8
127.0.0.1:6379> lrange list1 0 2
-8
1
0
127.0.0.1:6379> lset list1 3 -6 # 根据索引设置列表中元素的值,当list不存在时报错
ERR index out of range
# 从尾部插入
127.0.0.1:6379> lrange list1 0 2
-8
1
0
127.0.0.1:6379> rpush list1 haha # 从尾部插入
4
127.0.0.1:6379> llen list1
4
127.0.0.1:6379> lrange list1 0 3
-8
1
0
haha
# LREM key count value  #从存于 key 的列表里移除前 count 次出现的值为 value 的元素
# count > 0: 从头往尾移除值为 value 的元素
# count < 0: 从尾往头移除值为 value 的元素
# count = 0: 移除所有值为 value 的元素

127.0.0.1:6379> lrange list1 0 12 # 查看现有list
4
2
3
2
-8
1
haha
2
4
2
2
3
2
127.0.0.1:6379> lrem list1 2 2 # 从list中移除前2次出现的2
2
127.0.0.1:6379> lrange list1 0 10 # 查看移除后的结果
4
3
-8
1
haha
2
4
2
2
3
2
127.0.0.1:6379> lrem list1 -1 2 # 从list从尾往头移除2，移除1次
1
127.0.0.1:6379> lrange list1 0 9
4
3
-8
1
haha
2
4
2
2
3
127.0.0.1:6379> lrem list1 0 2 # count为0，移除所有的2
3
127.0.0.1:6379> lrange list1 0 9
4
3
-8
1
haha
4
3
127.0.0.1:6379> lpop list1  # 删除头部元素
4
127.0.0.1:6379> lrange list1 0 9
3
-8
1
haha
4
3
```
<a name="LbXn1"></a>
### list应用场景举例

1. 可以使用list来实现一个消息队列(如博客的评论内容), 确保先后顺序, 而不必像mysql那样使用`order by`来排序. 
1. 使用`lrange`还可以很方便地实现分页功能.
1. 页面上每次取最新的三个商品：左边添加，右边删除，每次显示3个
1. 若干人值班，每次轮流一次。
<a name="WXz3m"></a>
## 对set的操作
Redis 的 Set 是 String 类型的无序集合，其中的元素没有先后顺序。集合成员是唯一的，这就意味着集合中不能出现重复的数据。<br />Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。<br />集合中最大的成员数为 2 (4294967295, 每个集合可存储40多亿个成员)。<br />
<br />

<a name="qqlli"></a>
# 感谢
[https://blog.csdn.net/xc_zhou/article/details/80700602#t2](https://blog.csdn.net/xc_zhou/article/details/80700602#t2)<br />[https://www.cnblogs.com/wdliu/p/9360286.html?utm_source=tuicool&utm_medium=referral](https://www.cnblogs.com/wdliu/p/9360286.html?utm_source=tuicool&utm_medium=referral)

