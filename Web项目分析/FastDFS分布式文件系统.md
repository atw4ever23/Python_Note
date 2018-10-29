# FastDFS分布式文件系统

FastDFS 架构包括 **Tracker server** 和 **Storage server**

- **Tracker server** 作用是负载均衡和调度，通过 Tracker server 在文件上传时可以根据一些 策略找到 Storage server 提供文件上传服务。可以将 tracker 称为**追踪服务器**或**调度服务器**。
- **Storage server** 作用是文件存储，客户端上传的文件最终存储在 Storage 服务器上， Storageserver 没有实现自己的文件系统而是利用操作系统 的文件系统来管理文件。可以将 storage 称为**存储服务器**。

