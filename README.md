# 介绍
项目基于cppla版本ServerStatus， 增加如下功能：

- 更方便的节点管理, 支持增删改查
- 上下线通知（telegram）
- Agent机器安装脚本改为systemd， 支持开机自启

>由于未改动cppla版的任何代码，所以，我愿意把这个项目称为ServerStatus的小插件, 理论上它可以为任何版本的ServerStatus服务


# 安装
在**服务端**复制以下命令，一键到底。请记得替换成你自己的YOUR_TG_CHAT_ID和YOUR_TG_BOT_TOKEN。

其中，Bot token可以通过@BotFather创建机器人获取， Chat id可以通过@getuserID获取。

```
mkdir sss && cd sss && wget --no-check-certificate https://raw.githubusercontent.com/lidalao/ServerStatus/master/sss.sh && chmod +x ./sss.sh && sudo ./sss.sh YOUR_TG_CHAT_ID YOUR_TG_BOT_TOKEN

```
安装成功后，web服务地址：http://ip:8081

更多信息请移步 https://lidalao.com/archives/87  +1ip

由于没改动ServerStatus代码，理论上，任何版本的ServerStatus都可以用_sss.py来做管理， 都可以用bot.py来进行上下监控。

节点管理时，把_sss.py放到和config.json同一目录，运行python3 _sss.py即可。唯一需要改动的就是restartSSS函数，此函数功能是重启ServerStatus服务，改成你对应的服务启动方式，例如用systemd,则把["docker-compose", "restart"]改成["systemctl", "restart", "ServerStatus"]。

接下来是上下线监控服务，同样适用于任何版本的ServerStatus。 它只有一个文件bot.py, 可以跑在任何机器上，不是必须在服务端，丢在家里nas上也成。

bot.py里面有三个配置信息，bot_token, cat_id和NODE_STATUS_URL, 改成你自己的对应信息，NODE_STATUS_URL需要改成你自己的探针web服务地址，例如，域名探针https://tz.test.com, 则改为https://tz.test.com/json/stats.json。配置修改完后，运行python3 bot.py即可开始监控



# 参考
- https://github.com/cppla/ServerStatus
- https://github.com/naiba/nezha
