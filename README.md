##**Dtop自动化运维平台 1.0**
#####平台介绍
Dtop运维平台是集成了CMDB、自动化操作、配置系统、运维告警、流程管理、日志审计、权限管理、API接口与Dnspod远程管理等功能功能模块的一个综合性运维管理工具。后续还会纳入代码审核发布模块，该运维平台整体采用BS架构，批量运维部分采用CS架构，前端提供web界面，直观的提供展示与操作界面；
首页如下：
![aaa](/IMG/index.png)

***
#####环境介绍
使用的是python2.7，django版本：1.9.6，centos 6.5 x64位，暂不支持windows；


***
#####模块介绍&功能描述：
#####- CMDB模块：
主要涵盖云资源的在线管理、固定资产管理等，可实时对云资源进行采集；支持资产的增删改查，导入导出等；

![aaa](/IMG/cloud.png)

![aaa](/IMG/asset.png)

#####- 自动化管理：
基于CMDB采集的云资源，底层采用salt进行主客户端的交互，通过私钥认证的方式，灵活控制客户端的增删与匹配，实现web界面对选定linux客户端进行日常的运维操作；

![aaa](/IMG/op1.png)
![aaa](/IMG/op2.png)

#####- 运维告警：
目前采用zabbix api方式从公司的zabbix平台调取告警日志，web端实现弹窗告警；使得运维工程师能第一时间发现告警并及时处理；

![aaa](/IMG/alarm.png)

#####- 流程管理：
目前的流程管理仿照OA，即由用户发起流程，制定流程主办人，主办时间等，同时该流程抄送指定知会人；该流程只能由主办人进行处理，知会人只有知会权限；同时流程完成百分比通过前端不同颜色进度条进行区分；流程处理过程入库存档；

![aaa](/IMG/em1.png)

![aaa](/IMG/em2.png)

#####- 日志审计：
当前的日志审计针对所有的功能模块，用户的每次登陆、增删改查操作、运维操作指令、流程发起、处理、完结、Dnspod操作等，采用记录时间、用户、IP、执行模块、动作类型、操作详情等字段的方式记录每一次操作；实现真正的有踪可查；

#####- 权限管理：
web完成用户与用户组的新建，赋权；细化每个模块的具体操作权限；

![aaa](/IMG/auth.png)

#####- API接口：
遵循RESTful设计理念，利用Django REST framework构建运维管理平台的API，便于后续与其他系统的相互对接；

#####- Dnspod远程管理：
杜绝个人登录Dnspod进行操作，回收登录密码，全部通过该运维平台进行Dnspod管理；

![aaa](/IMG/DNS.png)

***

#####使用说明
可能需要额外安装的软件包：rpyc，xlwt等

将该源码包下载到linux环境下，配置好相应的数据库，将saltMaster文件夹的reloadSalt.sh与saltrpyc.py两个文件存放至salt主服务器上，赋予两个文件可执行权限，并设置定时任务防止saltrpyc脚本挂死。

每天凌晨重启saltrpyc客户端
`* 0 * * * sh /home/saltMaster/reloadSalt.sh >/dev/null 2>&1`


***
#####说明：该运维平台仍旧在开发当中，很多功能不稳定甚至暂未实现，本人也会不定期的更新该项目。

欢迎关注[我的博客园](http://www.cnblogs.com/mzpy1119/)
