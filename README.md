# frps-nginx-https
# nginx反代frps实现https的模板配置文件
## 服务器拓扑假设
![服务器拓扑假设]()
如上图所示，假设本地有两台服务器，一台nginx服务器负责本地网站的承载**下面称为LS1**，另一台负责运行frpc**下面称为LS2**，实际使用中这两台服务器可以合二为一，远端有一台frps服务器
## 可实现以下四种功能
1. （放在case1中）本地LS1正确配置http跳转到https(TLS)，远端frps直接监听80 443端口
2. （放在case2中）本地LS1正确配置http跳转到https(TLS)，远端nginx反代frps转发的https实现泛解析和http跳转到https，frps监听其他端口（适用于想要正确传递https客户端真实IP，由于frpc到frps线路质量不佳需要缓存，frps服务器同时需要挂其他网站等特殊需求）
3. （放在case3中）本地LS1只配置http，远端nginx反向代理frps转发的http到https，frps监听其他端口（是远端nginx反代的伪https，**极不推荐**，但如有本地特殊http需求或因为*懒癌晚期*本地确不想用https的请看本部分）
4. （放在case4中）本地LS1只配置http，远端nginx反向代理frps转发的http到http，frps监听其他端口
