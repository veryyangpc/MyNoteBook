# MyNoteBook
记录常见的软件安装问题
## elasticsearch-6.0.0 安装问题
### 问题1 max file descriptors [4096] for elasticsearch process likely too low, increase to at least [65536]
* 原因：无法创建本地文件问题,用户最大可创建文件数太小
* 解决方案：切换到root用户，编辑limits.conf配置文件， 添加类似如下内容：  
\* soft nofile 65536  
\* hard nofile 131072  
\* soft nproc 2048  
\* hard nproc 4096  
* 备注：\* 代表Linux所有用户名称（比如 hadoop）, 需要保存、退出、重新登录才可生效。
### 问题2 max number of threads [1024] for user [es] likely too low, increase to at least [2048]
* 原因：无法创建本地线程问题,用户最大可创建线程数太小
* 解决方案：切换到root用户，进入limits.d目录下，修改90-nproc.conf 配置文件，vi /etc/security/limits.d/90-nproc.conf
*找到如下内容：
\* soft nproc 1024
修改为
\* soft nproc 2048
### 问题3 max virtual memory areas vm.max_map_count [65530] likely too low, increase to at least [262144]
* 原因：最大虚拟内存太小  
* 解决方案：  
vi /etc/sysctl.conf  
vm.max_map_count=262144  
sysctl -p  
