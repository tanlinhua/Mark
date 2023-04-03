# HomeBrew

## 安装

```bash
/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"
```

## 常用命令

```
本地软件库列表 brew ls
查找软件 brew search google（其中google替换为要查找的关键字）
查看brew版本 brew -v  更新brew版本：brew update
安装cask软件 brew install --cask firefox 把firefox换成你要安装的
启动服务 brew services start redis@4.0
查看服务 brew services list
安装软件 brew install name
桌面端软件 brew cask install name
联网搜索软件是否存在brew中 brew search name
更新软件 brew upgrade name
查询可更新的包 brew outdated
卸载软件 brew uninstall name
重新安装软件 brew reinstall name
查看软件安装地址 brew info name
清理缓存 brew cleanup
查看建议，例如升级等 brew doctor
链接 brew link name
```

## Golang

```shell
brew install go
```

## ngnix

```shell
安装： brew install nginx
启动： brew services start nginx
重启： brew services restart nginx
停止： brew services stop nginx

查看安装目录： brew list nginx
检查配置： nginx -t

nginx配置tp5.0

vim /opt/homebrew/etc/nginx/servers/php-web-admin.conf

server {
        listen       1992;
        server_name  localhost;

        access_log  /Users/jason/Code/apps/nginx/logs/access.log;
        error_log   /Users/jason/Code/apps/nginx/logs/error.log;

        index index.php index.html index.htm;
    	root /Users/jason/Code/Php/PhpWebAdmin/public/;
    	location / {
		if (!-e $request_filename ) {
			rewrite ^(.*)$ /index.php?s=/$1 last;
			break;
		}
		 try_files $uri $uri/ /index.php?$args;
    	}
    	location ~ \.php$ {
		fastcgi_pass 127.0.0.1:9000;
		fastcgi_index index.php;
		fastcgi_split_path_info       ^(.+\.php)(/?.+)$;
            	fastcgi_param PATH_INFO       $fastcgi_path_info;
            	fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
            	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            	include                       fastcgi_params;
    	}
        location ~ /\.ht {
            deny  all;
        }
    }

nginx  重新加载配置|重启|停止|退出
nginx -s reload|reopen|stop|quit
nginx -t 测试配置是否有语法错误
```

## php

```
brew安装php

brew search php  使用此命令搜索可用的PHP版本
brew install php@7.4 使用此命令安装指定版本的php
brew install brew-php-switcher 安装php多版本切换工具
brew-php-switcher 7.4 切换PHP版本到7.4（需要brew安装多个版本）

php -v & php -m

启动php-fpm
brew services start php@7.4
or
/usr/local/opt/php@7.4/sbin/php-fpm --nodaemonize

brew安装PHP扩展

通过brew安装的PHP版本中自带了pecl,可以直接使用
pecl version 查看版本信息
pecl help 可以查看命令帮助
pecl search xdebug  搜索可以安装的扩展信息
pecl install xdebug 安装扩展
pecl install http://pecl.php.net/get/redis-4.2.0.tgz 安装指定版本扩展
默认扩展.so文件会被编译到/usr/local/Cellar/php@7.2/7.2.15/pecl/目录中，此目录实际上是软链接到了/usr/local/lib/php/pecl目录。

查看扩展是否开启的方法：
1. php -m
2. phpinfo()
3. extension_loaded() //直接判断扩展是否加载
4. function_exists() //判断扩展库下的方法是否存在
5. php --ri 扩展名 //查看扩展版本信息
```

### composer

```
1、composer查看全局设置：composer config -gl
2、查看已存在的包：composer info [***] or composer show [***]
3、搜索包：composer search ***
4、安装包：composer require或者composer install
	对于 require 和 install 是不相同的，require 会把包的信息添加到 composer.json 文件中并进行 install 。
	而 install 是直接从 composer.json 或 composer.lock 文件中提取依赖信息，然后进行安装。

	不编辑composer.json的情况下安装库:
	你可能会觉得每安装一个库都需要修改composer.json太麻烦，那么你可以直接使用require命令。
5、清理缓存：composer clearcache [composer cc]
6、依赖性检测：composer depends ***
7、设置composer镜像为国内镜像：
	composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
8、卸载某个扩展或者删除某个包：composer remove
	这只是删除了依赖关系，不会自动加载，但其依赖包还在vender文件夹里，可手动删除
9、诊断：composer diagnose
```

## mysql

如果之前没有安装过 MySQL 5.7

```
brew install mysql@5.7  // 安装
brew link --force mysql@5.7 // 链接
brew services start mysql@5.7 // 启动服务
echo 'export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"' >> ~/.zshrc // 输出到环境变量
```

如果之前安装了 MySQL 5.7

```
brew uninstall mysql@5.7
rm -rf /usr/local/var/mysql
rm /usr/local/etc/my.cnf

--- 👇和第一种情况一样

brew install mysql@5.7  // 安装
brew link --force mysql@5.7 // 链接
brew services start mysql@5.7 // 启动服务
echo 'export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"' >> ~/.zshrc // 输出到环境变量
```

❗️ 重要的一步，设置安全的访问

```
mysql_secure_installation
```

mysql 密码： root+root

## redis

```
brew install redis@4.0
```

## nodejs

```shell
brew install nvm

mkdir ~/.nvm

vim ~/.zshrc  在 ~/.zshrc 配置文件后添加如下内容
export NVM_DIR="$HOME/.nvm"
  [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"
  [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"

source ~/.zshrc
echo $NVM_DIR
nvm --help
nvm ls-remote

nvm install 14
nvm uninstall 14

nvm list 是查找本电脑上所有的node版本
nvm install <version> 安装指定版本node
nvm use <version> 切换使用指定的版本node
nvm ls 列出所有版本
nvm current 显示当前版本
nvm alias <name> <version> ## 给不同的版本号添加别名
nvm unalias <name> ## 删除已定义的别名
nvm reinstall-packages <version> ## 在当前版本node环境下，重新全局安装指定版本号的npm包
```

## Java

### JDK

```shell
brew install openjdk@11

sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk

.zshrc:

export JAVA_11_HOME="/Library/Java/JavaVirtualMachines/openjdk@11.jdk/Contents/Home"
alias java11='export JAVA_HOME=$JAVA_11_HOME'

export JAVA_19_HOME="/Library/Java/JavaVirtualMachines/openjdk.jdk/Contents/Home"
alias java19='export JAVA_HOME=$JAVA_19_HOME'

export JAVA_HOME=$JAVA_11_HOME

java11
java -version
java19
java -version
```

### Eclipse

[DevStyle Eclipse 超级好看的主题，极力推荐](https://blog.csdn.net/Thinkingcao/article/details/89499869)

[Eclipse+Spring boot 开发教程](https://www.cnblogs.com/lsdb/p/9783435.html)

### Maven

maven 缓存目录： ~/.m2

[mac maven](https://gitee.com/zhengqingya/java-developer-document/blob/master/%E7%9F%A5%E8%AF%86%E5%BA%93/Java/01-%E7%8E%AF%E5%A2%83/02-Maven/01-%E5%AE%89%E8%A3%85-mac.md)

```shell
brew install maven
```

### Android

[mac M1 安装 AndroidStudio 打开真机调试](https://blog.csdn.net/cungudafa/article/details/126743686)

gradle 缓存目录： ~/.gradle -> 4G 多

```shell
1.
brew install --cask android-platform-tools

2.android studio安装好之后提价path ↓
export PATH="$HOME/Android/sdk/platform-tools:$PATH"
export PATH="$HOME/Android/sdk/tools:$PATH"
```
