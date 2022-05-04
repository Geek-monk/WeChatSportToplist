# 十五锐行走，快马不能追。二十入山林，一去无还期。
[![刷步数-微信运动](https://github.com/Geek-monk/WeChatSportToplist/actions/workflows/run.yml/badge.svg)](https://github.com/Geek-monk/WeChatSportToplist/actions/workflows/run.yml)
![同步到Gitee](https://github.com/xunichanghuan/mimotion/actions/workflows/sync2gitee.yml/badge.svg)
![GitHub forks](https://img.shields.io/github/forks/Geek-monk/WeChatSportToplist?style=social)
![GitHub Repo stars](https://img.shields.io/github/stars/Geek-monk/WeChatSportToplist?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/Geek-monk/WeChatSportToplist?style=social)
![GitHub forks](https://img.shields.io/github/forks/Geek-monk/WeChatSportToplist?style=social)  
![python版本](https://img.shields.io/badge/Python-3.9-blue)
![IDE](https://img.shields.io/badge/IDE-Pycharm-green)
![测试平台](https://img.shields.io/badge/%E6%B5%8B%E8%AF%95%E5%B9%B3%E5%8F%B0-Android-yellowgreen)
## 使用小米运动自动刷步数

- 下载小米运动
- 注册账号 
- 设置密码
- 绑定微信
- 绑定支付宝

## Github Actions 部署指南

- 原理就是使用action持续部署，达到每天定时更新的目的。如果不会使用，请查看[官方文档](https://docs.github.com/cn/actions)

### 一、设置账号密码

- 按着如下表格将参数填入main.py

| Secrets |  格式  |
| -------- | ----- |
| USER |   小米运动登录账号,仅支持小米运动账号对应的手机号,不支持小米账号|
| PWD |   小米运动登录密码,仅支持小米运动账号对应的密码|
| SKEY |   酷推skey，如无填写**NO**|
| SCKEY |   server酱sckey，如无填写**NO**|
| POSITION |   是否开启企业微信推送**false**关闭,**true**开启|
| CORPID |   企业ID， 登陆企业微信，在我的企业-->企业信息里查看,必填，如果没有，填写**NO**|
| CORPSECRET |   自建应用，每个自建应用里都有单独的secret,必填，如果没有，填写**NO**|
| AGENTID |   填写你的应用ID，不加引号，是个整型常数,就是AgentId，如果没有，填写**NO**|
| TOUSER |   指定接收消息的成员，成员ID列表（多个接收者用”&#166;”分隔，最多支持1000个）。特殊情况：指定为”@all”，则向该企业应用的全部成员发送，如果没有，填写**NO**|
| TOPARTY |   指定接收消息的部门，部门ID列表，多个接收者用”&#166;”分隔，最多支持100个。当touser为”@all”时填写”@all”，如果没有，填写**NO**|
| TOTAG |   指定接收消息的标签，标签ID列表，多个接收者用”&#166;”分隔，最多支持100个。当touser为”@all”时填写”@all”，如果没有，填写**NO**|
| OPEN_GET_WEATHER |   开启根据地区天气情况降低步数**False**关闭,**True**开启|
| AREA |   设置获取天气的地区（上面开启后必填）如：**北京**，当**OPEN_GET_WEATHER**为**False**时填写**NO**|
| PAT |   此处**PAT**需要申请，值为github token，教程详见：https://www.jianshu.com/p/bb82b3ad1d11 ,需要repo和workflow权限,此项必填，避免git push的权限错误。 |

### 二、自定义启动时间多账户(用不上请忽略)

多账户请用 **#** 分割 然后保存到变量 **USER** 和 **PWD**

#### 例如

13800138000#13800138001 变量 USER

abc123qwe#abcqwe2 变量 PWD

### 三、自定义启动时间

编辑 **main.py**

找到 time_list项目，此数据为北京时间，默认表示为8点10点13点15点17点19点21点运行,如需修改，请修改time_list列表，如：time_list = [7, 9, 13, 15, 17, 19, 20]就表示为7点9点13点15点17点19点20点运行，Actions触发里面也要同步修改。
编辑 **random_cron.sh**
修改其中**if**语句的判断时间为UTC时间，即**北京时间-8**，如北京时间8点为UTC时间0点，需要运行的时间-8就是UTC时间

