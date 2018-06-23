[![Build Status][travis-badge]][travis-link]

* 在[github.com/FreshRSS/FreshRSS/](https://github.com/FreshRSS/FreshRSS/blob/master/README.md)查看文档以便获取正确的链接和图文。 
* [Version française](README.fr.md)
* [Version englis](README.md)

# FreshRSS
FreshRSS是一个自托管的RSS feed聚合器，类似[Leed](http://projet.idleman.fr/leed/)和[Kriss Feed](https://tontof.net/kriss/feed/).FreshRSS 基于 PHP 框架 Minz。

FreshRSS 轻量、易用、强大且可定制。
FreshRSS是一个多用户应用，同时支持游客模式。
FreshRSS支持通过[PubSubHubbub](https://github.com/pubsubhubbub/PubSubHubbub) 给支持的网站推送即时消息。
另外还有给移动端app准备的API，以及命令行操作接口[Command-Line Interface](cli/README.md).
最后, FreshRSS 支持通过 [扩展](#extensions) 来增强或者调整功能.

* 官网: https://freshrss.org
* Demo: https://demo.freshrss.org/
* License: [GNU AGPL 3](https://www.gnu.org/licenses/agpl-3.0.html)

![FreshRSS logo](docs/img/FreshRSS-logo.png)

# 发行记录
详见 [发行记录](../../releases).

## 关于分支
* 如果你希望得到一个稳定版本，那么就用 [master分支](https://github.com/FreshRSS/FreshRSS/tree/master/)
* 如果你乐意帮忙测试或者开发新功能，那[dev分支](https://github.com/FreshRSS/FreshRSS/tree/dev)就是给你准备的

# 声明
开发此应用是为了满足个人需求，所以不提供任何保证。欢迎大家提功能需求，错误报告，或者其他贡献。推荐方式是[开一个 issue](https://github.com/FreshRSS/FreshRSS/issues)，我们是一个友好的社区。

# 要求
* 一个运行Linux 或者 Windows的轻量级服务器。
	* 他甚至能在Raspberry Pi 1 上工作，并且做到响应时间1秒以内。
* 一个web server: 比如Apache2 (推荐), nginx, lighttpd (其他服务器都没测试过)
* PHP 5.3.8+ (推荐PHP 5.4+ , 或者 PHP 5.5+ 获得更好性能,  或者PHP 7 获得更更更好的性能)
	* 必须安装的扩展: [cURL](https://secure.php.net/curl), [DOM](https://secure.php.net/dom), [XML](https://secure.php.net/xml), [session](https://secure.php.net/session), [ctype](https://secure.php.net/ctype), and [PDO_MySQL](https://secure.php.net/pdo-mysql) or [PDO_SQLite](https://secure.php.net/pdo-sqlite) or [PDO_PGSQL](https://secure.php.net/pdo-pgsql)
	* 推荐安装的扩展: [JSON](https://secure.php.net/json), [GMP](https://secure.php.net/gmp) (for API access on platforms < 64 bits), [IDN](https://secure.php.net/intl.idn) (for Internationalized Domain Names), [mbstring](https://secure.php.net/mbstring) and/or [iconv](https://secure.php.net/iconv) (for charset conversion), [ZIP](https://secure.php.net/zip) (for import/export), [zlib](https://secure.php.net/zlib) (for compressed feeds)
* MySQL 5.5.3+ (推荐), 或者 SQLite 3.7.4+, 或者 PostgreSQL 9.2+
* 一个不要太落后的浏览器比如 Firefox / IceCat, Internet Explorer 11 / Edge, Chromium / Chrome, Opera, Safari.
	* 手机上也能用

![FreshRSS screenshot](docs/img/FreshRSS-screenshot.png)

# 文档
* https://freshrss.github.io/FreshRSS/en/（显然 是英文的）

# [安装](https://freshrss.github.io/FreshRSS/en/admins/02_Installation.html)
1. 通过git获取FreshRSS或者[下载archive](https://github.com/FreshRSS/FreshRSS/archive/master.zip)
2. 复制到你的服务器(对外只要暴露 `./p/` 文件夹)
3. 给web server的用户赋予`./data/`文件夹的写权限  
4. 通过浏览器访问FreshRSS，然后跟随引导完成安装设置
	* 或者用[命令行](cli/README.md)操作
5. 然后应该就搞定了 :) 如果你遇到问题了， 请[联系我们](https://github.com/FreshRSS/FreshRSS/issues).
6. 你可以在 [config.default.php](config.default.php)看到高级设置，然后修改这个文件 `data/config.php`.
7. 如果你用Apache, 开启 [`AllowEncodedSlashes`](https://httpd.apache.org/docs/trunk/mod/core.html#allowencodedslashes) 以便更好地兼容移动端.

关于安装和服务器配置的更多信息，可以看我们的[文档](https://freshrss.github.io/FreshRSS/en/admins/02_Installation.html).

## 自动安装
* [Docker](./Docker/)
* [![Cloudron](https://cloudron.io/img/button.svg)](https://cloudron.io/button.html?app=org.freshrss.cloudronapp)
* [![DP deploy](https://raw.githubusercontent.com/DFabric/DPlatform-ShellCore/gh-pages/img/deploy.png)](https://dfabric.github.io/DPlatform-ShellCore)
* [YunoHost](https://github.com/YunoHost-Apps/freshrss_ynh)

## 在Linux Debian/Ubuntu上的一个完整安装过程示例
```
# If you use an Apache Web server (otherwise you need another Web server)
sudo apt-get install apache2
sudo a2enmod headers expires rewrite ssl	#Apache modules

# For Ubuntu <= 15.10, Debian <= 8 Jessie
sudo apt-get install php5 php5-curl php5-gmp php5-intl php5-json php5-sqlite
sudo apt-get install libapache2-mod-php5	#For Apache
sudo apt-get install mysql-server mysql-client php5-mysql	#Optional MySQL database
sudo apt-get install postgresql php5-pgsql	#Optional PostgreSQL database

# For Ubuntu >= 16.04, Debian >= 9 Stretch
sudo apt install php php-curl php-gmp php-intl php-mbstring php-sqlite3 php-xml php-zip
sudo apt install libapache2-mod-php	#For Apache
sudo apt install mysql-server mysql-client php-mysql	#Optional MySQL database
sudo apt install postgresql php-pgsql	#Optional PostgreSQL database

# Restart Web server
sudo service apache2 restart

# For FreshRSS itself (git is optional if you manually download the installation files)
cd /usr/share/
sudo apt-get install git
sudo git clone https://github.com/FreshRSS/FreshRSS.git
cd FreshRSS

# If you want to use the development version of FreshRSS
sudo git checkout -b dev origin/dev

# Set the rights so that your Web server can access the files
sudo chown -R :www-data . && sudo chmod -R g+r . && sudo chmod -R g+w ./data/
# If you would like to allow updates from the Web interface
sudo chmod -R g+w .

# Publish FreshRSS in your public HTML directory
sudo ln -s /usr/share/FreshRSS/p /var/www/html/FreshRSS
# Navigate to http://example.net/FreshRSS to complete the installation
# (If you do it from localhost, you may have to adjust the setting of your public address later)
# or use the Command-Line Interface

# Update to a newer version of FreshRSS with git
cd /usr/share/FreshRSS
sudo git pull
sudo chown -R :www-data . && sudo chmod -R g+r . && sudo chmod -R g+w ./data/
```

查看更多git和命令行操作，看[命令行接口文档](cli/README.md).

## 权限控制
It is needed for the multi-user mode to limit access to FreshRSS. You can:
* use form authentication (needs JavaScript, and PHP 5.5+ recommended)
* use HTTP authentication supported by your web server
	* See [Apache documentation](https://httpd.apache.org/docs/trunk/howto/auth.html)
		* In that case, create a `./p/i/.htaccess` file with a matching `.htpasswd` file.

## 自动更新源
* You can add a Cron job to launch the update script.
Check the Cron documentation related to your distribution ([Debian/Ubuntu](https://help.ubuntu.com/community/CronHowto), [Red Hat/Fedora](https://fedoraproject.org/wiki/Administration_Guide_Draft/Cron), [Slackware](https://docs.slackware.com/fr:slackbook:process_control?#cron), [Gentoo](https://wiki.gentoo.org/wiki/Cron), [Arch Linux](https://wiki.archlinux.org/index.php/Cron)…).
It is a good idea to use the Web server user.
For instance, if you want to run the script every hour:

```
9 * * * * php /usr/share/FreshRSS/app/actualize_script.php > /tmp/FreshRSS.log 2>&1
```

### 在Debian / Ubuntu上操作示例
Create `/etc/cron.d/FreshRSS` with:

```
6,36 * * * * www-data php -f /usr/share/FreshRSS/app/actualize_script.php > /tmp/FreshRSS.log 2>&1
```


# 高级
* 出于安全考虑, 应该只对外暴露`./p/` 文件夹.
	* 尤其要注意`./data/` 文件夹包含重要的配置数据，绝不能对外暴露。
* The `./constants.php` file defines access to application folder. If you want to customize your installation, every thing happens here.
* 如果发生错误，可以在这里查看日志 `./data/users/*/log*.txt` .
	* The special folder `./data/users/_/` contains the part of the logs that are shared by all users.


# 备份
* 请保存 `./data/config.php`, 和 `./data/users/*/config.php` 文件
* 您可以通过网页或者[命令行](cli/README.md)导出 OPML 格式的订阅源备份
* 您可以用 [phpMyAdmin](https://www.phpmyadmin.net) 或者其他数据库工具导出文章:

```bash
mysqldump --skip-comments --disable-keys --user=<db_user> --password --host <db_host> --result-file=freshrss.dump.sql --databases <freshrss_db>
```


# 扩展
FreshRSS支持在他的核心功能之上，通过扩展，来进一步增强功能.详见[repository dedicated to those extensions](https://github.com/FreshRSS/Extensions).


# APIs 和 原生app

FreshRSS 支持通过Linux, Android, iOS, 和 OS X的原生应用来访问，因为它写了两套对接的api.

## Google Reader-like API

关于跟Google Reader适配的api的信息可以看这个文档 [mobile access](https://freshrss.github.io/FreshRSS/en/users/06_Mobile_access.html).

支持的客户端有:

* Android
	* [News+](https://play.google.com/store/apps/details?id=com.noinnion.android.newsplus) with [News+ Google Reader extension](https://play.google.com/store/apps/details?id=com.noinnion.android.newsplus.extension.google_reader) (Closed source)
	* [FeedMe 3.5.3+](https://play.google.com/store/apps/details?id=com.seazon.feedme) (Closed source)
	* [EasyRSS](https://github.com/Alkarex/EasyRSS) (Open source, [F-Droid](https://f-droid.org/packages/org.freshrss.easyrss/))
* GNU/Linux
	* [FeedReader 2.0+](https://jangernert.github.io/FeedReader/) (Open source)

## Fever API

文档看这个 [Fever API documentation](https://freshrss.github.io/FreshRSS/en/users/06_Fever_API.html) page.

支持的客户端有:

* iOS
	* [Fiery Feeds](https://itunes.apple.com/app/fiery-feeds-rss-reader/id1158763303) (Closed source)
	* [Unread](https://itunes.apple.com/app/unread-rss-reader/id1252376153) (Closed source)
* MacOS
	* [Readkit](https://itunes.apple.com/app/readkit/id588726889) (Closed source)


# 用到的类库
* [SimplePie](https://simplepie.org/)
* [MINZ](https://github.com/marienfressinaud/MINZ)
* [php-http-304](https://alexandre.alapetite.fr/doc-alex/php-http-304/)
* [jQuery](https://jquery.com/)
* [lib_opml](https://github.com/marienfressinaud/lib_opml)
* [jQuery Plugin Sticky-Kit](https://leafo.net/sticky-kit/)
* [keyboard_shortcuts](http://www.openjs.com/scripts/events/keyboard_shortcuts/)
* [flotr2](http://www.humblesoftware.com/flotr2)

## 可选的
* [bcrypt.js](https://github.com/dcodeIO/bcrypt.js)
* [phpQuery](https://github.com/phpquery/phpquery)

## 用来替代原生功能
* [Services_JSON](https://pear.php.net/pepr/pepr-proposal-show.php?id=198)
* [password_compat](https://github.com/ircmaxell/password_compat)

[travis-badge]:https://travis-ci.org/FreshRSS/FreshRSS.svg?branch=master
[travis-link]:https://travis-ci.org/FreshRSS/FreshRSS
