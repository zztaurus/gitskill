### 线上服务器日志存储步骤说明

1.项目通过dock中的logger功能将日志存储到514端口；

2.系统rsyslog监听514端口(/etc/rsyslog.conf);

2.1 将日志存储到/var/logs/*.log中(/etc/rsyslog.d/50-cherrypie.conf);

2.2 将日志转发给1514端口（/etc/rsyslog.d/30-forward.conf);

3.logd(http://git.ihandysoft.com/all-tech-server/lib_toolkit_server)监听1514端口，将日志分别存储到firehose和elasticsearch中；