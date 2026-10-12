## muduo_Chat

平台工具 ：Linux（Ubuntu）、VSCode 远程开发、CMake 构建系统、GDB 调试、Shell 自动化编译脚本  
项目内容：  
1、基于 muduo 网络库实现 RPC 服务端与客户端的 TCP 网络通信，利用 Reactor 多线程模型（4 个 I/O 线程）支持高并发 RPC 调用  
2、使用 Protobuf 定义服务接口与消息结构，实现 RPC 请求/响应的自动序列化与反序列化，解耦网络层与业务层  
3、自定义 RPC 协议头设计：header_size（4 字节定长） + RpcHeader（Protobuf 序列化，含 service_name/method_name/args_size） + args（Protobuf 序列化参数），解决 TCP 粘包问题  
4、集成 ZooKeeper 实现分布式服务注册与发现：Provider 启动时将服务名（永久节点）和方法名（临时节点，携带 IP:Port）注册到 ZK；Consumer 通过 ZK 查询服务地址，实现服务动态发现与负载均衡  
5、实现异步日志系统：采用生产者-消费者模式，基于互斥锁 + 条件变量实现线程安全队列，独立写日志线程以 detach 方式运行，避免日志 I/O 阻塞业务线程  
6、基于 Protobuf 的 Service/Stub 机制，实现 MprpcChannel 统一封装所有 RPC 调用的序列化与网络发送，MprpcController 管理 RPC 调用状态与错误信息  
7、实现配置解析模块：支持 key=value 格式配置文件，含注释过滤与空格 Trim，通过命令行参数 -i 指定配置文件路径  

#其它：待升级处：使用qt/electron进行页面化操作  
