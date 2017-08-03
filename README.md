## 斗鱼 定时弹幕助手

帮助你定时发送弹幕~~签到~~

### Installation

##### CentOS 7
1. 安装 PHP, Swoole 扩展
```sh
rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
```sh
yum --enablerepo=remi,remi-php71 install php php-common php-process php-pecl-swoole2 -y
```
2. 安装 Composer
```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```
```sh
php composer-setup.php --install-dir=/usr/bin
```
3. 安装项目，依赖
```sh
git clone https://github.com/meanevo/douyu-danmaku_checkin-helper.git && cd douyu-danmaku_checkin-helper
```
```sh
composer.phar install
```

### Usage
1. 打开浏览器登录斗鱼后，在 F12->Storage->Cookies 中找到 acf_uid, acf_stk, acf_ltkid 三个字段，记下备用
2. 配置 .env, 参考附录
3. 运行```php run.php```

### Appendix
#### env 配置
字段|State
-|-
LOG_LEVEL|日志等级，INFO: 显示弹幕消息，NOTICE: 屏蔽
DEVICE_ID|机器识别码，最好自己生成一个UUID，去除-后填入
AUTH_UID|对应 Cookie: acf_uid
AUTH_STK|对应 Cookie: acf_stk
AUTH_LTKID|对应 Cookie: acf_ltkid
ROOM_ID|房间号
SEND_MESSAGE|定时弹幕内容，${内解析为PHP语法} (Eg.设置为 "#签到 ${date('H:i')}" 时，发送 "#签到 15:30")
SEND_FROM|定时弹幕开始时间，配合时间间隔使用
SEND_INTERVAL|定时弹幕间隔（秒） (Eg.设置为1800时，若SEND_FROM=2017-08-01 05:33:11，当前时间=2017-08-01 05:00:00，则下一次弹幕发送时间为 05:33:11 + 00:30:00，之后为30分钟一次)