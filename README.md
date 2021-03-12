<p align=center>
    <img width=400 src="http://www.webfunny.cn/resource/logo-letter.png"/>
</p>


<p align="center">
  <a href="#项目大小"><img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/a597873885/webfunny_monitor"></a>
  <a href="#最近更新"><img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/a597873885/webfunny_monitor"></a>
  <a href="https://github.com/a597873885/webfunny_monitor/issues"><img alt="GitHub issues" src="https://img.shields.io/github/issues-raw/a597873885/webfunny_monitor"></a>
  <a href="https://github.com/a597873885/webfunny_monitor/issues?q=is%3Aissue+is%3Aclosed"><img alt="GitHub closed issues" src="https://img.shields.io/github/issues-closed-raw/a597873885/webfunny_monitor"></a>
  <a href="#开源协议"><img alt="GitHub" src="https://img.shields.io/github/license/a597873885/webfunny_monitor"></a>
</p>

> 如果你是一位前端工程师，那你一定不止一次去解决一些顽固的线上问题，你也曾想方设法复现用户的bug，结果可能都不太理想。 怎样定位前端线上问题，一直以来，都是很头疼的问题，因为它发生于用户的一系列操作之后。错误的原因可能源于机型，网络环境，复杂的操作行为等等，在我们想要去解决的时候很难复现出来，自然也就无法解决。

> 身为一名前端工程师，我每天都要面临很多线上的问题，一时间让我焦头烂额。公司其他的监控系统也有，但是每次解决问题都需要辗转于各种监控系统之间，亦是疲惫不堪。所以，我便为自己（前端工程师）量身定做了这样一款监控系统，现在分享给大家使用，欢迎点击了解。

> 只需要简单几步，你就可以搭建一套属于自己的前端监控系统了。

### 了解作品  

   [【官网简介】](http://www.webfunny.cn/home.html) | 
   [【Demo效果】](http://www.webfunny.cn/demo/home.html) | 
   [【更新日志】](http://www.webfunny.cn/update.html) |
   [【关于开源】](http://www.webfunny.cn/faq.html?tab=2)
 ### 联系作者微信

   微信号：webfunny_2020

   <img width=150 src="http://www.webfunny.cn/src/assets/img/wx_add.jpeg"/>
   

### 私有化部署方式
   
   [【Docker部署】](https://github.com/a597873885/webfunny_monitor/blob/master/DES_DOCKER.md)
   


### 基础环境

    安装NodeJS，版本号：10.6.0及以上

### 第一步、下载(clone)最新部署包，初始化（不要改项目名！！！）

    1.本地克隆代码$：git clone https://github.com/a597873885/webfunny_monitor.git

      使用码云仓库$：git clone https://gitee.com/webfunnyMonitor/webfunny_monitor.git（github网络不稳定，可以使用码云地址）
  
    2.在项目根目录下执行初始化命令和安装命令$：npm run init && npm install

    3.确认是否安装了pm2（执行$：pm2 -v），如果没有安装pm2，请执行安装命令$：npm install pm2 -g


### 第二步、配置数据库(Mysql)连接

<b>1. 安装 Mysql 数据库</b>（<a href="https://www.cnblogs.com/warm-stranger/p/10333348.html">Mysql安装教程</a>）

<b>2. 创建数据库</b>（webfunny_db）

    创建数据库：webfunny_db。

    字符集设置：[Default Character set]：utf8、 [Default Collation]：utf8_bin

#### 3. 数据库连接配置

进入webfunny_monitor/bin/mysqlConfig.js文件中
  
    module.exports = {
      write: {
        ip: 'xxx.xxx.xxx.xxx',         // 远程ip地址
        port: '3306',                  // 端口号
        dataBaseName: 'webfunny_db',   // 数据库名
        userName: 'root',              // 用户名
        password: '123456'             // 密码
      }
    }


### 第三步、本地部署运行


    1) 此时此刻，本地配置已经完成了，尝试运行命令$: npm run prd（第一次运行使用此命令，重启使用：npm run restart）

    2) 打开浏览器，访问地址：http://localhost:8010/webfunny/register.html?type=1 (初始化管理员账号，并登录)

    3) 创建新项目后，可以看到探针部署教程，完成部署。


### 第四步、生产环境部署

<b>1. IP地址或者域名配置</b>

进入webfunny_monitor/bin/domain.js文件中<b>（注意，对应的端口号要保持一致）</b>

    IP地址配置方式：

    module.exports = {
      localServerDomain: 'xxx.xxx.xxx.xxx:8011',    // 日志上报域名
      localAssetsDomain: 'xxx.xxx.xxx.xxx:8010',    // 前端页面域名
      localServerPort: '8011',                      // 日志上报端口号
      localAssetsPort: '8010',                      // 前端页面端口号
    }

    域名配置方式：

    module.exports = {
      localServerDomain: 'www.baidu.com:8011',      // 日志上报域名
      localAssetsDomain: 'www.baidu.com:8010',      // 前端页面域名
      localServerPort: '8011',                      // 日志上报端口号
      localAssetsPort: '8010',                      // 前端页面端口号
    }

配置完成后，浏览器访问以下地址，保证能够访问成功。

    1.项目列表地址，请在控制台执行：curl http://xxx.xxx.xxx.xxx:8011/server/webMonitorIdList 或 curl http://www.baidu.com:8011/server/webMonitorIdList

    2.数据展示地址，请在浏览器访问：http://xxx.xxx.xxx.xxx:8010/webfunny/overview.html 或 http://www.baidu.com:8010/webfunny/overview.html

------------

<b>2. 添加执行权限（重要！！！否则无法生成数据库表）</b>

正常情况下 createTable.sh, restart.sh 这两个脚本没有执行权限，需要用户手动授权。

    linux、mac系统，需要在项目根目录下执行命令$：chmod 755 createTable.sh， chmod 755 restart.sh 进行授权。

    其他操作系统，请自行搜索授权方式

    【注意】如果不授权，可能无法自动创建每天的数据库表


### 第五步、配置报警信息（钉钉机器人）

webfunny提供了自定义报警拦截功能，执行 npm run init 命令后会出现interceptor目录，需要使用者修改代码，以实现钉钉机器人的报警方式，配置目录如下：

    钉钉机器人配置文件：/interceptor/config/dingRobot.js，其他通知方式，请自己查看代码
--------------

以下步骤可不必执行，高并发的用户可以继续往下看。

--------------


### 第六步、启动消息队列(非必须)
#### 1. 安装RabbitMq（建议您在云服务器上部署完成后再执行此步骤）

    开启消息队列之前，请先 安装RabbitMq消息队列服务，ubantu：https://www.cnblogs.com/warm-stranger/p/11000996.html 

    安装完成后可以访问Url：http://IP地址:15672 查看消息队列的情况
    
    如果需要连接远程消息队列，请在根目录下找到 lib/RabbitMq.js调整代码配置。
    
    【小提示】：消息队列不易安装成功，如果中途出现问题，可以选择重启或者初始化云服务器。
#### 2. 启动消息队列

    RabbitMq 安装完成后，在 webfunny_monitor/bin/messageQueue.js 文件中找到变量名：messageQueue，将此变量的值设置为：true, 重启服务即可

### 第七步、配置读写分离(非必须)

    1.配置好主从同步的多台MySQL数据库（最好是一主多从，一主一从尚可）

    2.进入webfunny_monitor/bin/mysqlConfig.js文件中

    module.exports = {
      write: {
        ip: 'xxx.xxx.xxx.xxx',         // 远程ip地址
        port: '3306',                  // 端口号
        dataBaseName: 'webfunny_db',   // 数据库名
        userName: 'root',              // 用户名
        password: '123456'             // 密码
      }，
      // 高性能版支持此属性
      read: [
        { host: "xxx.xxx.xxx.xxx", username: "root1", password: "123456" },
        { host: "xxx.xxx.xxx.xxx", username: "root2", password: "123456" }
      ]
    }
